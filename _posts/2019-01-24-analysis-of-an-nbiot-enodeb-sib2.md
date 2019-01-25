---
layout: post
title: A Glimpse of the SIB2 of a Commercially-deployed NB-IoT eNodeB
description: SIB2 is the "System Information Block 2". It tells the UE about the parameters and configuration that are adopted by the eNodeB, so that the UE can communicate with the eNodeB successfully. Here is a simple analysis of a typical SIB2.
permalink: /analysis-of-an-nbiot-enodeb-sib2/
categories: [blog]
tags: [NB-IoT, eNodeB, SIB2, base station, 3GPP]
date: 2019-01-24 11:24:38 
---

# SIB2 File in `.asn` Format

The file that stores the SIB2 info:

[Download SIB2-2509.asn](../assets/post-img/analysis-of-an-nbiot-enodeb-sib2/SIB2-2509.asn)

You can download it and read on your computer.

Also, you can comment to correct any mistakes you found in this post.

# Structure Overview

Here is a list structure view.

-   BCCH-DL-SCH-Message-NB
    -   message c1 : systemInformation-r13
        -   criticalExtensions systemInformation-r13
            -   sib-TypeAndInfo-r13
                -   **sib2-r13**
                    -   **radioResourceConfigCommon-r13**
                        -   rach-ConfigCommon-r13
                        -   bcch-Config-r13
                        -   pcch-Config-r13
                        -   nprach-Config-r13
                        -   npdsch-ConfigCommon-r13
                        -   npusch-ConfigCommon-r13
                        -   uplinkPowerControlCommon-r13
                    -   ue-TimersAndConstants-r13
                    -   freqInfo-r13
                    -   timeAlignmentTimerCommon-r13
                -   sib3-r13
                -   sib5-r13

As we can see, most of the variable names end with "-r13", which means "Release 13". Among all the configurations, `radioResourceConfigCommon` is one of the most important. It characterizes all the channel behaviors.

# Units and Facts

All the configurations are in a <key, value> pair format. Most of the values have a unit. The strange thing is that the unit is put ahead of the numbers. For example, "ms1000" means 1000 milliseconds.

Here is the list of all the units used in SIB2:

-   `n`: number / integer
-   `dB`: decibel
-   `dBm`: power level w.r.t milliwatt (mW)
-   `pp`: number of consecutive subframes
-   `rf`: radio frame (10 ms)
-   `r`: number of repetitions
-   `us`: microsecond
-   `ms`: millisecond
-   `s`: ?
-   `v`: the index of the subframe

Facts:

-   If the variable has "List" in its name, it means you can specify multiple entities in it, usually corresponds to multiple enhanced coverage levels (ECL).

# radioResourceConfigCommon Details

The detailed explanation can be found in 3GPP TS 36.321.

## rach-ConfigCommon-r13

-   `preambleTransMax-CE`: maximum number of preamble transmission. The value is 6.
-   `powerRampingParameters`
    -   `powerRampingStep`: the power-ramping factor, the step size that the UE changes the TX power. The value is 2 dB.
    -   `preambleInitialReceivedTargetPower`: the initial preamble power. The value is -112 dBm.
-   `rach-InfoList`
    -   `ra-ResponseWindowSize`: UE should send the MSG3 after it receives the MSG2 within the window size. The value is 10 subframe (10 ms).
    -   `mac-ContentionResolutionTimer`: the time allowed to resolve the RA contention. If the UE doesn't get the MSG4 from the eNodeB before the timer expires, this RA fails. The value is 32 subframe (32 ms).

## bcch-Config-r13

-   `modificationPeriodCoeff`: the times that UE tries to detect any SIB changes. The value is 32.

## pcch-Config-r13

-   `defaultPagingCycle`: the UE should try to read the paging at least once during this cycle. The value is 256 radio frame (2560 ms).
-   `nB`: a parameter to derive the Paging Frame and Paging Occasion. the value is 1/8 \* T.
-   `npdcch-NumRepetitionPaging`: maximum number of repetitions for NPDCCH common search space (CSS) for paging. The value is 128.

## nprach-Config-r13 (An important part)

-   `nprach-CP-Length`: the cyclic prefix (CP) length of NPRACH. The value is 66.7 us.
-   `rsrp-ThresholdsPrachInfoList`: the thresholds for UEs to select a NPRACH resource. The first element should be greater than the second element. The list is [33, 23]. The unit of the elements is unknown yet.
-   `nprach-ParametersList`
    -   `nprach-Periodicity`: how often is an NPRACH frame. The value is 640 ms.
    -   `nprach-StartTime`: start time of the NPRACH resource. The values are 8, 64, 128 ms.
    -   `nprach-SubcarrierOffset`: frequency location of the NPRACH resource. The value is 36.
    -   `nprach-NumSubcarriers`: how many sub-carriers in the NPRACH resouce. The value is 12.
    -   `nprach-SubcarrierMSG3-RangeStart`: the fraction to calculate the starting subcarrier index. The value is one. Find more in 3GPP TS 36.331.
    -   `maxNumPreambleAttemptCE`: maximum number of preamble transmission attempts per NPRACH resource. The value is 4.
    -   `numRepetitionsPerPreambleAttempt`: repetition in each preamble attempt. The values are 2, 8, and 32.
    -   `npdcch-NumRepetitions-RA`: maximum number of repetitions for NPDCCH common search space (CSS) for RAR, Msg3 retransmission and Msg4. The values are 8, 16, and 128.
    -   `npdcch-StartSF-CSS-RA`: starting subframe configuration for NPDCCH common search space (CSS) for RAR, MSG3 RETX and MSG4. The value is 2.
    -   `npdcch-Offset-RA`: fractional period offset of starting subframe for NPDCCH CSS Type 2. The value is oneEighth.

## npdsch-ConfigCommon-r13

-   `nrs-Power`: the downlink NB reference signal EPRE, the unit is dBm. So the value is 29 dBm.

## npusch-ConfigCommon-r13

-   `ack-NACK-NumRepetitions-Msg4`: number of repetitions for the ACK NACK resource unit carrying HARQ response to NPDSCH. The values are 2, 4, and 64.
-   `ul-ReferenceSignalsNPUSCH`
    -   `groupHoppingEnabled`: enabling sequence-group hopping. The option is False.
    -   `groupAssignmentNPUSCH`: used to calculate the sequence-shift pattern. The value is 0.

## uplinkPowerControlCommon-r13

-   `p0-NominalNPUSCH`: the nominal power in uplink transmission. The value is -105 dBm.
-   `alpha`: a parameter for NPUSCH power calculation. al1 means 1.
-   `deltaPreambleMsg3`: parameters in calculating the nominal NPUSCH power. The value is 4.

# Other Parameters in SIB2

## ue-TimersAndConstants-r13

The detailed information can be found in Section 7.3.1 of 3GPP TS 36.331.

-   `t300`: the timer starts at RRCConnectionRequest or RRCConnectionResumeRequest transmission, stops at the reception of RRCConnectionSetup/Reject/Resume etc. The value is 10000 ms.
-   `t301`: records the time from RRCConnectionReestablishmentRequest to the acception or rejection response. The value is 25000 ms.
-   `t310`: records the time from detecting PHY layer problem to triggering handover or connection re-establishment. The value is 8000 ms.
-   `n310`: a constant, maximum number of consecutive "out-of-sync" or "early-out-of-sync" indications for the PCell received from lower layers. The value is 10.
-   `t311`: records the time from initiating the RRC connection re-establishment procedure to the selection of a suitable E-UTRA cell or a cell using another RAT. The value is 30000 ms.
-   `n311`: a constant, maximum number of consecutive "in-sync" or "early-in-sync" indications from the PCell received from lower layers. The value is 1.

## freqInfo-r13

-   `additionalSpectrumEmission`: a UE requirement. The value is 1.

## timeAlignmentTimerCommon-r13

I did not find much information about this. The value is infinity.

# Appendix

Full SIB2.

```json
00-80-01-A9-7C-F3-CA-AF-50-97-A8-66-49-96-B6-65-A1-2C-66-6B-92-C9-17-80-15-F4-EE-D8-01-C4-0F-20-19-26-10-10-27-25-43-00-81-39-AA-18-80-00-00-00-00-00-00-00-00-00-00

008001A97CF3CAAF5097A8664996B665A12C666B92C9178015F4EED801C40F2019261010272543008139AA188000000000000000000000
BCCH-DL-SCH-Message-NB:
{
  message c1 : systemInformation-r13 : 
  {
    criticalExtensions systemInformation-r13 : 
    {
      sib-TypeAndInfo-r13 
      {
        sib2-r13 : 
        {
          radioResourceConfigCommon-r13 
          {
            rach-ConfigCommon-r13 
            {
              preambleTransMax-CE-r13 n6,
              powerRampingParameters-r13 
              {
                powerRampingStep dB2,
                preambleInitialReceivedTargetPower dBm-112
              },
              rach-InfoList-r13 
              {
                {
                  ra-ResponseWindowSize-r13 pp10,
                  mac-ContentionResolutionTimer-r13 pp32
                },
                {
                  ra-ResponseWindowSize-r13 pp5,
                  mac-ContentionResolutionTimer-r13 pp32
                },
                {
                  ra-ResponseWindowSize-r13 pp5,
                  mac-ContentionResolutionTimer-r13 pp32
                }
              }
            },
            bcch-Config-r13 
            {
              modificationPeriodCoeff-r13 n32
            },
            pcch-Config-r13 
            {
              defaultPagingCycle-r13 rf256,
              nB-r13 one8thT,
              npdcch-NumRepetitionPaging-r13 r128
            },
            nprach-Config-r13 
            {
              nprach-CP-Length-r13 us66dot7,
              rsrp-ThresholdsPrachInfoList-r13 
              {
                33,
                23
              },
              nprach-ParametersList-r13 
              {
                {
                  nprach-Periodicity-r13 ms640,
                  nprach-StartTime-r13 ms8,
                  nprach-SubcarrierOffset-r13 n36,
                  nprach-NumSubcarriers-r13 n12,
                  nprach-SubcarrierMSG3-RangeStart-r13 one,
                  maxNumPreambleAttemptCE-r13 n4,
                  numRepetitionsPerPreambleAttempt-r13 n2,
                  npdcch-NumRepetitions-RA-r13 r8,
                  npdcch-StartSF-CSS-RA-r13 v2,
                  npdcch-Offset-RA-r13 oneEighth
                },
                {
                  nprach-Periodicity-r13 ms640,
                  nprach-StartTime-r13 ms64,
                  nprach-SubcarrierOffset-r13 n36,
                  nprach-NumSubcarriers-r13 n12,
                  nprach-SubcarrierMSG3-RangeStart-r13 one,
                  maxNumPreambleAttemptCE-r13 n4,
                  numRepetitionsPerPreambleAttempt-r13 n8,
                  npdcch-NumRepetitions-RA-r13 r16,
                  npdcch-StartSF-CSS-RA-r13 v2,
                  npdcch-Offset-RA-r13 zero
                },
                {
                  nprach-Periodicity-r13 ms640,
                  nprach-StartTime-r13 ms128,
                  nprach-SubcarrierOffset-r13 n36,
                  nprach-NumSubcarriers-r13 n12,
                  nprach-SubcarrierMSG3-RangeStart-r13 one,
                  maxNumPreambleAttemptCE-r13 n4,
                  numRepetitionsPerPreambleAttempt-r13 n32,
                  npdcch-NumRepetitions-RA-r13 r128,
                  npdcch-StartSF-CSS-RA-r13 v2,
                  npdcch-Offset-RA-r13 zero
                }
              }
            },
            npdsch-ConfigCommon-r13 
            {
              nrs-Power-r13 29
            },
            npusch-ConfigCommon-r13 
            {
              ack-NACK-NumRepetitions-Msg4-r13 
              {
                r2,
                r8,
                r64
              },
              ul-ReferenceSignalsNPUSCH-r13 
              {
                groupHoppingEnabled-r13 FALSE,
                groupAssignmentNPUSCH-r13 0
              }
            },
            uplinkPowerControlCommon-r13 
            {
              p0-NominalNPUSCH-r13 -105,
              alpha-r13 al1,
              deltaPreambleMsg3-r13 4
            }
          },
          ue-TimersAndConstants-r13 
          {
            t300-r13 ms10000,
            t301-r13 ms25000,
            t310-r13 ms8000,
            n310-r13 n10,
            t311-r13 ms30000,
            n311-r13 n1
          },
          freqInfo-r13 
          {
            additionalSpectrumEmission-r13 1
          },
          timeAlignmentTimerCommon-r13 infinity
        },
        sib3-r13 : 
        {
          cellReselectionInfoCommon-r13 
          {
            q-Hyst-r13 dB3
          },
          cellReselectionServingFreqInfo-r13 
          {
            s-NonIntraSearch-r13 25
          },
          intraFreqCellReselectionInfo-r13 
          {
            q-RxLevMin-r13 -70,
            s-IntraSearchP-r13 25,
            t-Reselection-r13 s3
          }
        },
        sib5-r13 : 
        {
          interFreqCarrierFreqList-r13 
          {
            {
              dl-CarrierFreq-r13 
              {
                carrierFreq-r13 2505,
                carrierFreqOffset-r13 v-0dot5
              },
              q-RxLevMin-r13 -64
            },
            {
              dl-CarrierFreq-r13 
              {
                carrierFreq-r13 2509,
                carrierFreqOffset-r13 v-0dot5
              },
              q-RxLevMin-r13 -64
            }
          },
          t-Reselection-r13 s3
        }
      }
    }
  }
}
```
