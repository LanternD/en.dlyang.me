---
layout: post
title: Learning srsLTE - 2
description: srsLTE data structure overview and references. Include ASN.1, interfaces, radio and upper.
permalink: /learning-srslte-2/
categories: [blog]
tags: [srslte, software radio, software, library]
date: 2018-03-22 17:34:56
---

# Introduction

There are so many API provided by srsLTE library. One can find an API document of srsLTE provided by the well-known [ShareTechNote](http://www.sharetechnote.com/) website, including

-   [API description](http://www.sharetechnote.com/html/SDR_srsLTE_Api.html)
-   [Data structure description](http://www.sharetechnote.com/html/SDR_srsLTE_Api_TypeDef.html)

Though the website is comprehensive and detailed, I think the web page was not well-rendered, especially the code. Using sans-serif non-monospaced fonts for the code is not a good practice, isn't it? By the way, the data structure page does not have anchor links to navigate.

In this document, I will give a reference to the structure type definition. I'll leave the API functions to the following posts.

**`struct` and `enum` type only. Classes are not included.**

**Physical layer data structure will be in another post!**

**If I think some data structure is not important (at the time I write the post), or I'm too lazy, I will put them in "Other data structure defined in this file".**

# Shortcuts

## ASN.1

asdf &vert; ax | dff \\| xcf | zxcv

## Common

## Interfaces

## Radio

## Upper

# Data Structures

## ASN.1

ASN.1 means "Abstract Syntax Notation One". See more at [Wikipedia](https://en.wikipedia.org/wiki/Abstract_Syntax_Notation_One).

---

### gtpc\_header

Location: `./lib/include/srslte/asn1/gtpc.h`

```c++
typedef struct gtpc_header
{
  uint8_t version;
  bool piggyback;
  bool teid_present;
  uint8_t type;
  uint64_t teid;
  uint64_t sequence;
} gtpc_header_t;
```

Read more: [GPRS Tunnelling Protocol - Wikipedia](https://en.wikipedia.org/wiki/GPRS_Tunnelling_Protocol).

### gtpc\_msg\_choice

Location: `./lib/include/srslte/asn1/gtpc.h`

```c++
typedef union gtpc_msg_choice
{
  struct gtpc_create_session_request create_session_request;
  struct gtpc_create_session_response create_session_response;
  struct gtpc_modify_bearer_request modify_bearer_request;
  struct gtpc_modify_bearer_response modify_bearer_response;
  struct gtpc_delete_session_request delete_session_request;
  struct gtpc_delete_session_response delete_session_response;
} gtpc_msg_choice_t; 
```

### gtpc\_pdu

Location: `./lib/include/srslte/asn1/gtpc.h`

```c++
typedef struct gtpc_pdu
{
  struct gtpc_header header;
  union gtpc_msg_choice choice;
} gtpc_pdu_t;
```

### gtpc\_cause\_ie

Location: `./lib/include/srslte/asn1/gtpc_ies.h`

```c++
struct gtpc_cause_ie
{
  enum gtpc_cause_value cause_value;
  bool pce;
  bool bce;
  bool cs;
  enum gtpc_ie_type offending_ie_type;
  uint16_t length_of_offending_ie;
  uint8_t offending_ie_instance;
};
```

Other data structure defined in this file: `enum gtpc_ie_type`, `enum gtpc_cause_value`, `struct gtpc_ambr_ie`, `enum gtpc_pdn_type`, `struct gtpc_pdn_address_allocation_ie`, `enum gtpc_rat_type`, `enum gtpc_interface_type`, `struct gtpc_f_teid_ie`.

### gtpc\_create\_session\_request

Location: `./lib/include/srslte/asn1/gtpc_msg.h`

```c++
struct gtpc_create_session_request
{
  bool imsi_present;
  uint64_t imsi;   						// C

  enum gtpc_rat_type rat_type;					// M

  struct gtpc_f_teid_ie sender_f_teid;					// M
  bool pgw_addr_present;
  struct gtpc_f_teid_ie pgw_addr;					// C

  char apn[MAX_APN_LENGTH];							// M

  struct gtpc_bearer_context_created_ie //see  TS 29.274 v10.14.0 Table 7.2.1-2
  {
    uint8_t ebi;
    bool tft_present;
    bool s1_u_enodeb_f_teid_present;
    struct gtpc_f_teid_ie s1_u_enodeb_f_teid;
    bool s4_u_sgsn_f_teid_present;
    struct gtpc_f_teid_ie s4_u_sgsn_f_teid;
    bool s5_s8_u_sgw_f_teid_present;
    struct gtpc_f_teid_ie s5_s8_u_sgw_f_teid;
    bool s5_s8_u_pgw_f_teid_present;
    struct gtpc_f_teid_ie s5_s8_u_pgw_f_teid;
    bool s12_rnc_f_teid_present;
    struct gtpc_f_teid_ie s12_rnc_f_teid;
    bool s2b_u_epdg_f_teid_present;
    struct gtpc_f_teid_ie s2b_u_epdg_f_teid;
  } eps_bearer_context_created;		// M
};
```

Other data structure defined in this file: `struct gtpc_create_session_response`, `struct gtpc_modify_bearer_request`, `struct gtpc_modify_bearer_response`, `struct gtpc_delete_session_request`, `struct gtpc_delete_session_response`.

### LIBLTE\_ERROR\_ENUM

Location: `./lib/include/srslte/asn1/liblte_common.h`

```c++
typedef enum{
  LIBLTE_SUCCESS = 0,
  LIBLTE_ERROR_INVALID_INPUTS,
  LIBLTE_ERROR_ENCODE_FAIL,
  LIBLTE_ERROR_DECODE_FAIL,
  LIBLTE_ERROR_INVALID_CRC,
  LIBLTE_ERROR_N_ITEMS
}LIBLTE_ERROR_ENUM;
```

### LIBLTE\_ASN1\_OID\_STRUCT

Location: `./lib/include/srslte/asn1/liblte_common.h`

```c++
typedef struct {
   uint32_t numids;                             // number of subidentifiers
   uint32_t subid[LIBLTE_ASN1_OID_MAXSUBIDS];   // subidentifier values
} LIBLTE_ASN1_OID_STRUCT;
```

### LIBLTE\_BOOL\_MSG\_STRUCT

Location: `./lib/include/srslte/asn1/liblte_common.h`

```c++
typedef struct{
    bool   data_valid;
    bool   data;
}LIBLTE_BOOL_MSG_STRUCT;
```

### LIBLTE\_SIMPLE\_BIT\_MSG\_STRUCT

Location: `./lib/include/srslte/asn1/liblte_common.h`

```c++
typedef struct{

    uint32 N_bits;
    uint8  msg[LIBLTE_MAX_MSG_SIZE_BITS];
}LIBLTE_SIMPLE_BIT_MSG_STRUCT;
```

### LIBLTE\_SIMPLE\_BYTE\_MSG\_STRUCT

Location: `./lib/include/srslte/asn1/liblte_common.h`

```c++
typedef struct{
    uint32 N_bytes;
    uint8  msg[LIBLTE_MAX_MSG_SIZE_BYTES];
}LIBLTE_SIMPLE_BYTE_MSG_STRUCT;
```

### LIBLTE\_BYTE\_MSG\_STRUCT

Location: `./lib/include/srslte/asn1/liblte_common.h`

```c++
struct LIBLTE_BYTE_MSG_STRUCT{
    uint32  N_bytes;
    uint8   buffer[LIBLTE_MAX_MSG_SIZE_BYTES];
    uint8  *msg;

    LIBLTE_BYTE_MSG_STRUCT():N_bytes(0)
    {
      msg = &buffer[LIBLTE_MSG_HEADER_OFFSET];
    }
    LIBLTE_BYTE_MSG_STRUCT(const LIBLTE_BYTE_MSG_STRUCT& buf)
    {
      N_bytes = buf.N_bytes;
      memcpy(msg, buf.msg, N_bytes);
    }
    LIBLTE_BYTE_MSG_STRUCT & operator= (const LIBLTE_BYTE_MSG_STRUCT & buf)
    {
      // avoid self assignment
      if (&buf == this)
        return *this;
      N_bytes = buf.N_bytes;
      memcpy(msg, buf.msg, N_bytes);
      return *this;
    }
    uint32 get_headroom()
    {
      return msg-buffer;
    }
    void reset()
    {
      N_bytes = 0;
      msg = &buffer[LIBLTE_MSG_HEADER_OFFSET];
    }
};
```

### LIBLTE\_BIT\_MSG\_STRUCT

Location: `./lib/include/srslte/asn1/liblte_common.h`

```c++
struct LIBLTE_BIT_MSG_STRUCT{
    uint32  N_bits;
    uint8   buffer[LIBLTE_MAX_MSG_SIZE_BITS];
    uint8  *msg;

    LIBLTE_BIT_MSG_STRUCT():N_bits(0)
    {
      msg = &buffer[LIBLTE_MSG_HEADER_OFFSET];
      while( (uint64_t)(msg) % 8 > 0) {
        msg++;
      }
    }
    LIBLTE_BIT_MSG_STRUCT(const LIBLTE_BIT_MSG_STRUCT& buf){
      N_bits = buf.N_bits;
      memcpy(msg, buf.msg, N_bits);
    }
    LIBLTE_BIT_MSG_STRUCT & operator= (const LIBLTE_BIT_MSG_STRUCT & buf){
      // avoid self assignment
      if (&buf == this)
        return *this;
      N_bits = buf.N_bits;
      memcpy(msg, buf.msg, N_bits);
      return *this;
    }
    uint32 get_headroom()
    {
      return msg-buffer;
    }
    void reset()
    {
      N_bits = 0;
      msg = &buffer[LIBLTE_MSG_HEADER_OFFSET];
      while( (uint64_t)(msg) % 8 > 0) {
        msg++;
      }
    }
};
```

### LIBLTE\_MME\_DEVICE\_PROPERTIES\_ENUM

Location: `./lib/include/srslte/asn1/liblte_mme.h`

```c++
typedef enum{
    LIBLTE_MME_DEVICE_PROPERTIES_NOT_CONFIGURED_FOR_LOW_PRIORITY = 0,
    LIBLTE_MME_DEVICE_PROPERTIES_CONFIGURED_FOR_LOW_PRIORITY,
    LIBLTE_MME_DEVICE_PROPERTIES_N_ITEMS,
}LIBLTE_MME_DEVICE_PROPERTIES_ENUM;
```

`liblte_mme.h` is an important library that defines the common data structure for srsEPC part.

The remaining data structure list is soooo long (about 4,000 lines code) that I don't want to include them at this moment. I will add them whenever I access them in the code exploration.

### LIBLTE\_RRC\_NOTIFICATION\_REPETITION\_COEFF\_R9\_ENUM

Location: `./lib/include/srslte/asn1/liblte_rrc.h`

```c++
typedef enum{
    LIBLTE_RRC_NOTIFICATION_REPETITION_COEFF_R9_N2 = 0,
    LIBLTE_RRC_NOTIFICATION_REPETITION_COEFF_R9_N4,
    LIBLTE_RRC_NOTIFICATION_REPETITION_COEFF_R9_N_ITEMS,
}LIBLTE_RRC_NOTIFICATION_REPETITION_COEFF_R9_ENUM;
```

The remaining data structure list is soooo long (about 7,000 lines code) that I don't want to include them at this moment. I will add them whenever I access them in the code exploration.

### LIBLTE\_S1AP\_PROC\_ENUM

Location: `./lib/include/srslte/asn1/liblte_s1ap.h`

```c++
typedef enum{
  LIBLTE_S1AP_PROC_ID_HANDOVERPREPARATION                             = 0,
  LIBLTE_S1AP_PROC_ID_HANDOVERRESOURCEALLOCATION                      = 1,
  LIBLTE_S1AP_PROC_ID_HANDOVERNOTIFICATION                            = 2,
  LIBLTE_S1AP_PROC_ID_PATHSWITCHREQUEST                               = 3,
  LIBLTE_S1AP_PROC_ID_HANDOVERCANCEL                                  = 4,
  LIBLTE_S1AP_PROC_ID_E_RABSETUP                                      = 5,
  LIBLTE_S1AP_PROC_ID_E_RABMODIFY                                     = 6,
  LIBLTE_S1AP_PROC_ID_E_RABRELEASE                                    = 7,
  LIBLTE_S1AP_PROC_ID_E_RABRELEASEINDICATION                          = 8,
  LIBLTE_S1AP_PROC_ID_INITIALCONTEXTSETUP                             = 9,
  LIBLTE_S1AP_PROC_ID_PAGING                                          = 10,
  LIBLTE_S1AP_PROC_ID_DOWNLINKNASTRANSPORT                            = 11,
  LIBLTE_S1AP_PROC_ID_INITIALUEMESSAGE                                = 12,
  LIBLTE_S1AP_PROC_ID_UPLINKNASTRANSPORT                              = 13,
  LIBLTE_S1AP_PROC_ID_RESET                                           = 14,
  LIBLTE_S1AP_PROC_ID_ERRORINDICATION                                 = 15,
  LIBLTE_S1AP_PROC_ID_NASNONDELIVERYINDICATION                        = 16,
  LIBLTE_S1AP_PROC_ID_S1SETUP                                         = 17,
  LIBLTE_S1AP_PROC_ID_UECONTEXTRELEASEREQUEST                         = 18,
  LIBLTE_S1AP_PROC_ID_DOWNLINKS1CDMA2000TUNNELING                     = 19,
  LIBLTE_S1AP_PROC_ID_UPLINKS1CDMA2000TUNNELING                       = 20,
  LIBLTE_S1AP_PROC_ID_UECONTEXTMODIFICATION                           = 21,
  LIBLTE_S1AP_PROC_ID_UECAPABILITYINFOINDICATION                      = 22,
  LIBLTE_S1AP_PROC_ID_UECONTEXTRELEASE                                = 23,
  LIBLTE_S1AP_PROC_ID_ENBSTATUSTRANSFER                               = 24,
  LIBLTE_S1AP_PROC_ID_MMESTATUSTRANSFER                               = 25,
  LIBLTE_S1AP_PROC_ID_DEACTIVATETRACE                                 = 26,
  LIBLTE_S1AP_PROC_ID_TRACESTART                                      = 27,
  LIBLTE_S1AP_PROC_ID_TRACEFAILUREINDICATION                          = 28,
  LIBLTE_S1AP_PROC_ID_ENBCONFIGURATIONUPDATE                          = 29,
  LIBLTE_S1AP_PROC_ID_MMECONFIGURATIONUPDATE                          = 30,
  LIBLTE_S1AP_PROC_ID_LOCATIONREPORTINGCONTROL                        = 31,
  LIBLTE_S1AP_PROC_ID_LOCATIONREPORTINGFAILUREINDICATION              = 32,
  LIBLTE_S1AP_PROC_ID_LOCATIONREPORT                                  = 33,
  LIBLTE_S1AP_PROC_ID_OVERLOADSTART                                   = 34,
  LIBLTE_S1AP_PROC_ID_OVERLOADSTOP                                    = 35,
  LIBLTE_S1AP_PROC_ID_WRITEREPLACEWARNING                             = 36,
  LIBLTE_S1AP_PROC_ID_ENBDIRECTINFORMATIONTRANSFER                    = 37,
  LIBLTE_S1AP_PROC_ID_MMEDIRECTINFORMATIONTRANSFER                    = 38,
  LIBLTE_S1AP_PROC_ID_PRIVATEMESSAGE                                  = 39,
  LIBLTE_S1AP_PROC_ID_ENBCONFIGURATIONTRANSFER                        = 40,
  LIBLTE_S1AP_PROC_ID_MMECONFIGURATIONTRANSFER                        = 41,
  LIBLTE_S1AP_PROC_ID_CELLTRAFFICTRACE                                = 42,
  LIBLTE_S1AP_PROC_ID_KILL                                            = 43,
  LIBLTE_S1AP_PROC_ID_DOWNLINKUEASSOCIATEDLPPATRANSPORT               = 44,
  LIBLTE_S1AP_PROC_ID_UPLINKUEASSOCIATEDLPPATRANSPORT                 = 45,
  LIBLTE_S1AP_PROC_ID_DOWNLINKNONUEASSOCIATEDLPPATRANSPORT            = 46,
  LIBLTE_S1AP_PROC_ID_UPLINKNONUEASSOCIATEDLPPATRANSPORT              = 47,
  LIBLTE_S1AP_PROC_ID_UERADIOCAPABILITYMATCH                          = 48,
  LIBLTE_S1AP_PROC_ID_PWSRESTARTINDICATION                            = 49,
  LIBLTE_S1AP_PROC_N_ITEMS,
}LIBLTE_S1AP_PROC_ENUM;
```

The remaining data structure list is soooo long (about 10,300 lines code) that I don't want to include them at this moment. I will add them whenever I access them in the code exploration.

## Common

### error\_t

Location: `./lib/include/srslte/common/common.h`

```c++
typedef enum{
  ERROR_NONE = 0,
  ERROR_INVALID_PARAMS,
  ERROR_INVALID_COMMAND,
  ERROR_OUT_OF_BOUNDS,
  ERROR_CANT_START,
  ERROR_ALREADY_STARTED,
  ERROR_N_ITEMS,
}error_t;
```

### bit\_buffer\_t

Location: `./lib/include/srslte/common/common.h`

```c++
struct bit_buffer_t{
    uint32_t    N_bits;
    uint8_t     buffer[SRSLTE_MAX_BUFFER_SIZE_BITS];
    uint8_t    *msg;
#ifdef SRSLTE_BUFFER_POOL_LOG_ENABLED
    char        debug_name[128];
#endif

    bit_buffer_t():N_bits(0)
    {
      msg = &buffer[SRSLTE_BUFFER_HEADER_OFFSET];
    }
    bit_buffer_t(const bit_buffer_t& buf){
      N_bits = buf.N_bits;
      memcpy(msg, buf.msg, N_bits);
    }
    bit_buffer_t & operator= (const bit_buffer_t & buf){
      // avoid self assignment
      if (&buf == this)
        return *this;
      N_bits = buf.N_bits;
      memcpy(msg, buf.msg, N_bits);
      return *this;
    }
    void reset()
    {
      msg       = &buffer[SRSLTE_BUFFER_HEADER_OFFSET];
      N_bits    = 0;
      timestamp_is_set = false; 
    }
    uint32_t get_headroom()
    {
      return msg-buffer;
    }
    long get_latency_us()
    {
      if(!timestamp_is_set)
        return 0;
      gettimeofday(&timestamp[2], NULL); 
      return timestamp[0].tv_usec;
    }
    void set_timestamp() 
    {
      gettimeofday(&timestamp[1], NULL); 
      timestamp_is_set = true; 
    }

private: 
    struct timeval timestamp[3];
    bool           timestamp_is_set; 

};
```

### srslte\_nas\_config\_t

Location: `./lib/include/srslte/common/interfaces_common.h`

```c++
class srslte_nas_config_t
{
public:
  srslte_nas_config_t(uint32_t lcid_ = 0, std::string apn_ = "")
    :lcid(lcid_),
     apn(apn_)
    {}

  uint32_t    lcid;
  std::string apn;
};
```

### srslte\_gw\_config\_t

Location: `./lib/include/srslte/common/interfaces_common.h`

```c++
class srslte_gw_config_t
{
public:
  srslte_gw_config_t(uint32_t lcid_ = 0)
  :lcid(lcid_)
  {}

  uint32_t lcid;
};
```

### srslte\_pdcp\_config\_t

Location: `./lib/include/srslte/common/interfaces_common.h`

```c++
class srslte_pdcp_config_t
{
public:
  srslte_pdcp_config_t(bool is_control_ = false, bool is_data_ = false, uint8_t direction_ = SECURITY_DIRECTION_UPLINK)
    :direction(direction_)
    ,is_control(is_control_)
    ,is_data(is_data_)
    ,sn_len(12) {}

  uint8_t  direction;
  bool     is_control;
  bool     is_data;
  uint8_t  sn_len;

  // TODO: Support the following configurations
  // bool do_rohc;
};

```

### mac\_interface\_timers

Location: `./lib/include/srslte/common/interfaces_common.h`

```c++
class mac_interface_timers
{
public: 
  /* Timer services with ms resolution. 
   * timer_id must be lower than MAC_NOF_UPPER_TIMERS
   */
  virtual timers::timer* timer_get(uint32_t timer_id)  = 0;
  virtual void           timer_release_id(uint32_t timer_id) = 0;
  virtual uint32_t       timer_get_unique_id() = 0;
};

class read_pdu_interface
{
public:
  virtual int read_pdu(uint32_t lcid, uint8_t *payload, uint32_t requested_bytes) = 0;
};
```

### read\_pdu\_interface

Location: `./lib/include/srslte/common/interfaces_common.h`

```c++
class read_pdu_interface
{
public:
  virtual int read_pdu(uint32_t lcid, uint8_t *payload, uint32_t requested_bytes) = 0;
};
```

### liblte\_security\_generate\_k\_asme

Location: `./lib/include/srslte/common/liblte_security.h`

```c++
LIBLTE_ERROR_ENUM liblte_security_generate_k_asme(uint8  *ck,
                                                  uint8  *ik,
                                                  uint8  *ak,
                                                  uint8  *sqn,
                                                  uint16  mcc,
                                                  uint16  mnc,
                                                  uint8  *k_asme);
```

Generate the security key K\_asme. Reference: [33.401 v10.0.0 Annex A.2](http://www.etsi.org/deliver/etsi_ts/133400_133499/133401/10.00.00_60/ts_133401v100000p.pdf).

### liblte\_security\_generate\_k\_enb

Location: `./lib/include/srslte/common/liblte_security.h`

```c++
LIBLTE_ERROR_ENUM liblte_security_generate_k_enb(uint8  *k_asme,
                                                 uint32  nas_count,
                                                 uint8  *k_enb);
```

Generate the security key K\_enb. Reference: [33.401 v10.0.0 Annex A.3](http://www.etsi.org/deliver/etsi_ts/133400_133499/133401/10.00.00_60/ts_133401v100000p.pdf).

### liblte\_security\_generate\_k\_enb\_star

Location: `./lib/include/srslte/common/liblte_security.h`

```c++
LIBLTE_ERROR_ENUM liblte_security_generate_k_enb_star(uint8  *k_enb,
                                                      uint32  pci,
                                                      uint32_t earfcn,
                                                      uint8  *k_enb_star);
```

Reference: [33.401 v10.0.0 Annex A.5](http://www.etsi.org/deliver/etsi_ts/133400_133499/133401/10.00.00_60/ts_133401v100000p.pdf).

### liblte\_security\_generate\_nh

Location: `./lib/include/srslte/common/liblte_security.h`

```c++
LIBLTE_ERROR_ENUM liblte_security_generate_nh( uint8_t *k_asme,
                                               uint8_t *sync,
                                               uint8_t *nh);
```

Reference: [33.401 v10.0.0 Annex A.4](http://www.etsi.org/deliver/etsi_ts/133400_133499/133401/10.00.00_60/ts_133401v100000p.pdf).

### LIBLTE\_SECURITY\_CIPHERING\_ALGORITHM\_ID\_ENUM

Location: `./lib/include/srslte/common/liblte_security.h`

```c++
typedef enum{
    LIBLTE_SECURITY_CIPHERING_ALGORITHM_ID_EEA0 = 0,
    LIBLTE_SECURITY_CIPHERING_ALGORITHM_ID_128_EEA1,
    LIBLTE_SECURITY_CIPHERING_ALGORITHM_ID_128_EEA2,
    LIBLTE_SECURITY_CIPHERING_ALGORITHM_ID_N_ITEMS,
}LIBLTE_SECURITY_CIPHERING_ALGORITHM_ID_ENUM;
```

### LIBLTE\_SECURITY\_INTEGRITY\_ALGORITHM\_ID\_ENUM

Location: `./lib/include/srslte/common/liblte_security.h`

```c++
typedef enum{
    LIBLTE_SECURITY_INTEGRITY_ALGORITHM_ID_EIA0 = 0,
    LIBLTE_SECURITY_INTEGRITY_ALGORITHM_ID_128_EIA1,
    LIBLTE_SECURITY_INTEGRITY_ALGORITHM_ID_128_EIA2,
    LIBLTE_SECURITY_INTEGRITY_ALGORITHM_ID_N_ITEMS,
}LIBLTE_SECURITY_INTEGRITY_ALGORITHM_ID_ENUM;
```

### liblte\_security\_generate\_k\_nas

Location: `./lib/include/srslte/common/liblte_security.h`

```c++
LIBLTE_ERROR_ENUM liblte_security_generate_k_nas(uint8                                       *k_asme,
                                                 LIBLTE_SECURITY_CIPHERING_ALGORITHM_ID_ENUM  enc_alg_id,
                                                 LIBLTE_SECURITY_INTEGRITY_ALGORITHM_ID_ENUM  int_alg_id,
                                                 uint8                                       *k_nas_enc,
                                                 uint8                                       *k_nas_int);
```

Generate the NAS security keys KNASenc and KNASint. Reference: [33.401 v10.0.0 Annex A.7](http://www.etsi.org/deliver/etsi_ts/133400_133499/133401/10.00.00_60/ts_133401v100000p.pdf).

### liblte\_security\_generate\_k\_rrc

Location: `./lib/include/srslte/common/liblte_security.h`

```c++
LIBLTE_ERROR_ENUM liblte_security_generate_k_rrc(uint8                                       *k_enb,
                                                 LIBLTE_SECURITY_CIPHERING_ALGORITHM_ID_ENUM  enc_alg_id,
                                                 LIBLTE_SECURITY_INTEGRITY_ALGORITHM_ID_ENUM  int_alg_id,
                                                 uint8                                       *k_rrc_enc,
                                                 uint8                                       *k_rrc_int);
```

Generate the RRC security keys K\_RRCenc and K\_RRCint. Reference: [33.401 v10.0.0 Annex A.7](http://www.etsi.org/deliver/etsi_ts/133400_133499/133401/10.00.00_60/ts_133401v100000p.pdf).

### liblte\_security\_generate\_k\_up

Location: `./lib/include/srslte/common/liblte_security.h`

```c++
LIBLTE_ERROR_ENUM liblte_security_generate_k_up(uint8                                       *k_enb,
                                                LIBLTE_SECURITY_CIPHERING_ALGORITHM_ID_ENUM  enc_alg_id,
                                                LIBLTE_SECURITY_INTEGRITY_ALGORITHM_ID_ENUM  int_alg_id,
                                                uint8                                       *k_up_enc,
                                                uint8                                       *k_up_int);
```

Generate the user plane security keys K\_UPenc and K\_UPint. Reference: [33.401 v10.0.0 Annex A.7](http://www.etsi.org/deliver/etsi_ts/133400_133499/133401/10.00.00_60/ts_133401v100000p.pdf).

### liblte\_security\_128\_eia2

Location: `./lib/include/srslte/common/liblte_security.h`

```c++
LIBLTE_ERROR_ENUM liblte_security_128_eia2(uint8  *key,
                                           uint32  count,
                                           uint8   bearer,
                                           uint8   direction,
                                           uint8  *msg,
                                           uint32  msg_len,
                                           uint8  *mac);
```

128-bit integrity algorithm EIA2. Reference: [33.401 v10.0.0 Annex B.2.3](http://www.etsi.org/deliver/etsi_ts/133400_133499/133401/10.00.00_60/ts_133401v100000p.pdf), [33.102 v10.0.0 Section 6.5.4 RFC4493](http://www.etsi.org/deliver/etsi_ts/133100_133199/133102/10.00.00_60/ts_133102v100000p.pdf).

### liblte\_security\_128\_eia2

Location: `./lib/include/srslte/common/liblte_security.h`

```c++
LIBLTE_ERROR_ENUM liblte_security_128_eia2(uint8                 *key,
                                           uint32                 count,
                                           uint8                  bearer,
                                           uint8                  direction,
                                           LIBLTE_BIT_MSG_STRUCT *msg,
                                           uint8                 *mac);
```

### liblte\_security\_encryption\_eea1

Location: `./lib/include/srslte/common/liblte_security.h`

```c++
LIBLTE_ERROR_ENUM liblte_security_encryption_eea1(uint8  *key,
                                                  uint32  count,
                                                  uint8   bearer,
                                                  uint8   direction,
                                                  uint8  *msg,
                                                  uint32  msg_len,
                                                  uint8  *out);
```

128-bit encryption algorithm EEA1. Reference: [33.401 v13.1.0 Annex B.1.2 (Page 76)](http://www.etsi.org/deliver/etsi_ts/133400_133499/133401/13.01.00_60/ts_133401v130100p.pdf), 35.215 v13.0.0 References, Specification of the 3GPP Confidentiality and Integrity Algorithms UEA2 & UIA2 D1 v2.1.

### liblte\_security\_decryption\_eea1

Location: `./lib/include/srslte/common/liblte_security.h`

```c++
LIBLTE_ERROR_ENUM liblte_security_decryption_eea1(uint8  *key,
                                                  uint32  count,
                                                  uint8   bearer,
                                                  uint8   direction,
                                                  uint8  *ct,
                                                  uint32  ct_len,
                                                  uint8  *out);
```

128-bit decryption algorithm EEA1. Reference: 33.401 v13.1.0 Annex B.1.2, 35.215 v13.0.0 References Specification of the 3GPP Confidentiality and Integrity Algorithms UEA2 & UIA2 D1 v2.1.

### liblte\_security\_encryption\_eea2

Location: `./lib/include/srslte/common/liblte_security.h`

```c++
LIBLTE_ERROR_ENUM liblte_security_encryption_eea2(uint8  *key,
                                                  uint32  count,
                                                  uint8   bearer,
                                                  uint8   direction,
                                                  uint8  *msg,
                                                  uint32  msg_len,
                                                  uint8  *out);
```

128-bit encryption algorithm EEA2. Reference: [33.401 v13.1.0 Annex B.1.3 (Page 76)](http://www.etsi.org/deliver/etsi_ts/133400_133499/133401/13.01.00_60/ts_133401v130100p.pdf).

### liblte\_security\_milenage\_f1

Location: `./lib/include/srslte/common/liblte_security.h`

```c++
LIBLTE_ERROR_ENUM liblte_security_milenage_f1(uint8 *k,
                                              uint8 *op,
                                              uint8 *rand,
                                              uint8 *sqn,
                                              uint8 *amf,
                                              uint8 *mac_a);
```

Milenage security function F1. Computes network authentication code MAC-A from key K, random challenge RAND, sequence number SQN, and authentication management field AMF. Reference: [35.206 v10.0.0 Annex 3 (Page 18)](http://www.qtc.jp/3GPP/Specs/35206-a00.pdf).

### liblte\_security\_milenage\_f1\_star

Location: `./lib/include/srslte/common/liblte_security.h`

```c++
LIBLTE_ERROR_ENUM liblte_security_milenage_f1_star(uint8 *k,
                                                   uint8 *op,
                                                   uint8 *rand,
                                                   uint8 *sqn,
                                                   uint8 *amf,
                                                   uint8 *mac_s);
```

Milenage security function F1\*. Computes resynch authentication code MAC-S from key K, random challenge RAND, sequence number SQN, and authentication management field AMF. Reference: [35.206 v10.0.0 Annex 3 (Page 18)](http://www.qtc.jp/3GPP/Specs/35206-a00.pdf).

### liblte\_security\_milenage\_f2345

Location: `./lib/include/srslte/common/liblte_security.h`

```c++
LIBLTE_ERROR_ENUM liblte_security_milenage_f2345(uint8 *k,
                                                 uint8 *op,
                                                 uint8 *rand,
                                                 uint8 *res,
                                                 uint8 *ck,
                                                 uint8 *ik,
                                                 uint8 *ak);
```

Milenage security functions F2, F3, F4, and F5. Computes response RES, confidentiality key CK, integrity key IK, and anonymity key AK from random challenge RAND. Reference: [35.206 v10.0.0 Annex 3 (Page 18)](http://www.qtc.jp/3GPP/Specs/35206-a00.pdf).

### liblte\_security\_milenage\_f5\_star

Location: `./lib/include/srslte/common/liblte_security.h`

```c++
LIBLTE_ERROR_ENUM liblte_security_milenage_f5_star(uint8 *k,
                                                   uint8 *op,
                                                   uint8 *rand,
                                                   uint8 *ak);
```

Milenage security function F5\*. Computes resync anonymity key AK from key K and random challenge RAND. Reference: [35.206 v10.0.0 Annex 3 (Page 18)](http://www.qtc.jp/3GPP/Specs/35206-a00.pdf).

### LOG\_LEVEL\_ENUM

Location: `./lib/include/srslte/common/log.h`

```c++
typedef enum {
  LOG_LEVEL_NONE = 0,
  LOG_LEVEL_ERROR,
  LOG_LEVEL_WARNING,
  LOG_LEVEL_INFO,
  LOG_LEVEL_DEBUG,
  LOG_LEVEL_N_ITEMS
} LOG_LEVEL_ENUM;
```

### pcap\_hdr\_s

Location: `./lib/include/srslte/common/pcap.h`

```c++
typedef struct pcap_hdr_s {
        unsigned int   magic_number;   /* magic number */
        unsigned short version_major;  /* major version number */
        unsigned short version_minor;  /* minor version number */
        unsigned int   thiszone;       /* GMT to local correction */
        unsigned int   sigfigs;        /* accuracy of timestamps */
        unsigned int   snaplen;        /* max length of captured packets, in octets */
        unsigned int   network;        /* data link type */
} pcap_hdr_t;
```

This structure gets written to the start of the file.

### pcaprec\_hdr\_s

Location: `./lib/include/srslte/common/pcap.h`

```c++
typedef struct pcaprec_hdr_s {
        unsigned int   ts_sec;         /* timestamp seconds */
        unsigned int   ts_usec;        /* timestamp microseconds */
        unsigned int   incl_len;       /* number of octets of packet saved in file */
        unsigned int   orig_len;       /* actual length of packet */
} pcaprec_hdr_t;
```

This structure precedes each packet.

### MAC\_Context\_Info\_t

Location: `./lib/include/srslte/common/pcap.h`

```c++
typedef struct MAC_Context_Info_t {
    unsigned short radioType;
    unsigned char  direction;
    unsigned char  rntiType;
    unsigned short rnti;
    unsigned short ueid;
    unsigned char  isRetx;
    unsigned char  crcStatusOK;

    unsigned short sysFrameNumber;
    unsigned short subFrameNumber;
} MAC_Context_Info_t;
```

Context information for every MAC PDU (Protocol Data Unit) that will be logged.

### NAS\_Context\_Info\_t

Location: `./lib/include/srslte/common/pcap.h`

```c++
typedef struct NAS_Context_Info_s {
  // No Context yet
} NAS_Context_Info_t;
```

Context information for every NAS PDU that will be logged.

### CIPHERING\_ALGORITHM\_ID\_ENUM

Location: `./lib/include/srslte/common/security.h`

```c++
typedef enum{
    CIPHERING_ALGORITHM_ID_EEA0 = 0,
    CIPHERING_ALGORITHM_ID_128_EEA1,
    CIPHERING_ALGORITHM_ID_128_EEA2,
    CIPHERING_ALGORITHM_ID_N_ITEMS,
}CIPHERING_ALGORITHM_ID_ENUM;
```

### INTEGRITY\_ALGORITHM\_ID\_ENUM

Location: `./lib/include/srslte/common/security.h`

```c++
typedef enum{
    INTEGRITY_ALGORITHM_ID_EIA0 = 0,
    INTEGRITY_ALGORITHM_ID_128_EIA1,
    INTEGRITY_ALGORITHM_ID_128_EIA2,
    INTEGRITY_ALGORITHM_ID_N_ITEMS,
}INTEGRITY_ALGORITHM_ID_ENUM;
```

## Interfaces

### rf\_metrics\_t

Location: `./lib/include/srslte/interfaces/enb_metrics_interface.h`

```c++
typedef struct {
  uint32_t rf_o;
  uint32_t rf_u;
  uint32_t rf_l;
  bool     rf_error;
}rf_metrics_t;
```

### enb\_metrics\_t

Location: `./lib/include/srslte/interfaces/enb_metrics_interface.h`

```c++
typedef struct {
  rf_metrics_t    rf;
  phy_metrics_t   phy[ENB_METRICS_MAX_USERS];
  mac_metrics_t   mac[ENB_METRICS_MAX_USERS];
  rrc_metrics_t   rrc; 
  s1ap_metrics_t  s1ap;
  bool            running;
}enb_metrics_t;
```

### phy\_args\_t

Location: `./lib/include/srslte/interfaces/ue_interfaces.h`

```c++
typedef struct {
  bool ul_pwr_ctrl_en; 
  float prach_gain;
  int pdsch_max_its;
  bool attach_enable_64qam; 
  int nof_phy_threads;

  int worker_cpu_mask;
  int sync_cpu_affinity;

  uint32_t nof_rx_ant;
  std::string equalizer_mode;
  int cqi_max; 
  int cqi_fixed; 
  float snr_ema_coeff; 
  std::string snr_estim_alg; 
  bool cfo_integer_enabled; 
  float cfo_correct_tol_hz;
  float cfo_pss_ema;
  float cfo_ref_ema;
  float cfo_loop_bw_pss;
  float cfo_loop_bw_ref;
  float cfo_loop_ref_min;
  float cfo_loop_pss_tol;
  uint32_t cfo_loop_pss_conv;
  uint32_t cfo_ref_mask;
  bool average_subframe_enabled;
  int time_correct_period; 
  bool sfo_correct_disable; 
  std::string sss_algorithm; 
  float estimator_fil_w;   
  bool rssi_sensor_enabled;
  bool sic_pss_enabled;
} phy_args_t; 
```

UE physical layer arguments.

## Radio

### rf\_cal\_t

Location: `./lib/include/srslte/radio/radio.h`

```c++
typedef struct {
  float         tx_corr_dc_gain;
  float         tx_corr_dc_phase;
  float         tx_corr_iq_i;
  float         tx_corr_iq_q; 
  float         rx_corr_dc_gain;
  float         rx_corr_dc_phase;
  float         rx_corr_iq_i;
  float         rx_corr_iq_q; 
}rf_cal_t; 
```

## Upper

### gtpu\_header\_t

Location: `./lib/include/srslte/upper/gtpu.h`

```c++
typedef struct{
  uint8_t   flags;          // Only support 0x30 - v1, PT1 (GTP), no other flags
  uint8_t   message_type;   // Only support 0xFF - T-PDU type
  uint16_t  length;
  uint32_t  teid;
}gtpu_header_t;
```

### pdcp\_d\_c\_t

Location: `./lib/include/srslte/upper/pdcp_entity.h`

```c++
typedef enum{
    PDCP_D_C_CONTROL_PDU = 0,
    PDCP_D_C_DATA_PDU,
    PDCP_D_C_N_ITEMS,
}pdcp_d_c_t;
```

### rlc\_amd\_rx\_pdu\_t

Location: `./lib/include/srslte/upper/rlc_am.h`

```c++
struct rlc_amd_rx_pdu_t{
  rlc_amd_pdu_header_t  header;
  byte_buffer_t         *buf;
};
```

### rlc\_amd\_rx\_pdu\_segments\_t

Location: `./lib/include/srslte/upper/rlc_am.h`

```c++
struct rlc_amd_rx_pdu_segments_t{
  std::list<rlc_amd_rx_pdu_t> segments;
};
```

### rlc\_amd\_tx\_pdu\_t

Location: `./lib/include/srslte/upper/rlc_am.h`

```c++
struct rlc_amd_tx_pdu_t{
  rlc_amd_pdu_header_t  header;
  byte_buffer_t        *buf;
  uint32_t              retx_count;
  bool                  is_acked;
};
```

### rlc\_amd\_retx\_t

Location: `./lib/include/srslte/upper/rlc_am.h`

```c++
struct rlc_amd_retx_t{
  uint32_t  sn;
  bool      is_segment;
  uint32_t  so_start;
  uint32_t  so_end;
};
```

### rlc\_mode\_t

Location: `./lib/include/srslte/upper/rlc_common.h`

```c++
typedef enum{
  RLC_MODE_TM = 0,
  RLC_MODE_UM,
  RLC_MODE_AM,
  RLC_MODE_N_ITEMS,
}rlc_mode_t;
```

### rlc\_fi\_field\_t

Location: `./lib/include/srslte/upper/rlc_common.h`

```c++
typedef enum{
  RLC_FI_FIELD_START_AND_END_ALIGNED = 0,
  RLC_FI_FIELD_NOT_END_ALIGNED,
  RLC_FI_FIELD_NOT_START_ALIGNED,
  RLC_FI_FIELD_NOT_START_OR_END_ALIGNED,
  RLC_FI_FIELD_N_ITEMS,
}rlc_fi_field_t;
```

### rlc\_dc\_field\_t

Location: `./lib/include/srslte/upper/rlc_common.h`

```c++
typedef enum{
  RLC_DC_FIELD_CONTROL_PDU = 0,
  RLC_DC_FIELD_DATA_PDU,
  RLC_DC_FIELD_N_ITEMS,
}rlc_dc_field_t;
```

### rlc\_umd\_pdu\_header\_t

Location: `./lib/include/srslte/upper/rlc_common.h`

```c++
typedef struct{
  uint8_t           fi;                     // Framing info
  rlc_umd_sn_size_t sn_size;                // Sequence number size (5 or 10 bits)
  uint16_t          sn;                     // Sequence number
  uint32_t          N_li;                   // Number of length indicators
  uint16_t          li[RLC_AM_WINDOW_SIZE]; // Array of length indicators
}rlc_umd_pdu_header_t;
```

UMD PDU header.

### rlc\_amd\_pdu\_header\_t

Location: `./lib/include/srslte/upper/rlc_common.h`

```c++
struct rlc_amd_pdu_header_t{
  rlc_dc_field_t dc;                      // Data or control
  uint8_t        rf;                      // Resegmentation flag
  uint8_t        p;                       // Polling bit
  uint8_t        fi;                      // Framing info
  uint16_t       sn;                      // Sequence number
  uint8_t        lsf;                     // Last segment flag
  uint16_t       so;                      // Segment offset
  uint32_t       N_li;                    // Number of length indicators
  uint16_t       li[RLC_AM_WINDOW_SIZE];  // Array of length indicators

  rlc_amd_pdu_header_t(){
    dc = RLC_DC_FIELD_CONTROL_PDU;
    rf = 0; 
    p  = 0; 
    fi = 0; 
    sn = 0; 
    lsf = 0; 
    so = 0; 
    N_li=0;
    for(int i=0;i<RLC_AM_WINDOW_SIZE;i++)
      li[i] = 0;
  }
  rlc_amd_pdu_header_t(const rlc_amd_pdu_header_t& h)
  {
    copy(h);
  }
  rlc_amd_pdu_header_t& operator= (const rlc_amd_pdu_header_t& h)
  {
    copy(h);
    return *this;
  }
  void copy(const rlc_amd_pdu_header_t& h)
  {
    dc   = h.dc;
    rf   = h.rf;
    p    = h.p;
    fi   = h.fi;
    sn   = h.sn;
    lsf  = h.lsf;
    so   = h.so;
    N_li = h.N_li;
    for(uint32_t i=0;i<h.N_li;i++)
      li[i] = h.li[i];
  }
};
```

AMD PDU header.

### rlc\_status\_nack\_t

Location: `./lib/include/srslte/upper/rlc_common.h`

```c++
struct rlc_status_nack_t{
  uint16_t nack_sn;
  bool     has_so;
  uint16_t so_start;
  uint16_t so_end;

  rlc_status_nack_t(){has_so=false; nack_sn=0; so_start=0; so_end=0;}
};
```

NACK helper.

### rlc\_status\_pdu\_t

Location: `./lib/include/srslte/upper/rlc_common.h`

```c++
struct rlc_status_pdu_t{
  uint16_t          ack_sn;
  uint32_t          N_nack;
  rlc_status_nack_t nacks[RLC_AM_WINDOW_SIZE];

  rlc_status_pdu_t(){N_nack=0; ack_sn=0;}
};
```

Status PDU

### rlc\_umd\_sn\_size\_t

Location: `./lib/include/srslte/upper/rlc_interface.h`

```c++
typedef enum{
  RLC_UMD_SN_SIZE_5_BITS = 0,
  RLC_UMD_SN_SIZE_10_BITS,
  RLC_UMD_SN_SIZE_N_ITEMS,
}rlc_umd_sn_size_t;
```

### srslte\_rlc\_am\_config\_t

Location: `./lib/include/srslte/upper/rlc_interface.h`

```c++
typedef struct {
  /****************************************************************************
   * Configurable parameters
   * Ref: 3GPP TS 36.322 v10.0.0 Section 7
   ***************************************************************************/

  // TX configs
  int32_t    t_poll_retx;      // Poll retx timeout (ms)
  int32_t    poll_pdu;         // Insert poll bit after this many PDUs
  int32_t    poll_byte;        // Insert poll bit after this much data (KB)
  uint32_t   max_retx_thresh;  // Max number of retx

  // RX configs
  int32_t   t_reordering;       // Timer used by rx to detect PDU loss  (ms)
  int32_t   t_status_prohibit;  // Timer used by rx to prohibit tx of status PDU (ms)
} srslte_rlc_am_config_t;
```

### srslte\_rlc\_um\_config\_t

Location: `./lib/include/srslte/upper/rlc_interface.h`

```c++
typedef struct {
  /****************************************************************************
  * Configurable parameters
  * Ref: 3GPP TS 36.322 v10.0.0 Section 7
  ***************************************************************************/

  int32_t           t_reordering;       // Timer used by rx to detect PDU loss  (ms)
  rlc_umd_sn_size_t tx_sn_field_length; // Number of bits used for tx (UL) sequence number
  rlc_umd_sn_size_t rx_sn_field_length; // Number of bits used for rx (DL) sequence number

  uint32_t          rx_window_size;
  uint32_t          rx_mod;             // Rx counter modulus
  uint32_t          tx_mod;             // Tx counter modulus
} srslte_rlc_um_config_t;
```

### rlc\_metrics\_t

Location: `./lib/include/srslte/upper/rlc_metrics.h`

```c++
struct rlc_metrics_t
{
  float dl_tput_mbps;
  float ul_tput_mbps;
};
```

### rlc\_umd\_pdu\_t

Location: `./lib/include/srslte/upper/rlc_um.h`

```c++
struct rlc_umd_pdu_t{
  rlc_umd_pdu_header_t  header;
  byte_buffer_t        *buf;
};
```
