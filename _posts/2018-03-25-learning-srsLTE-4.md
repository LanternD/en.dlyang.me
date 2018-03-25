---
layout: post
title: Learning srsLTE - 4
description: srsLTE data structure overview and references. Physical channels layer data structure only.
permalink: /learning-srslte-4/
categories: [blog]
tags: [srslte, software radio, software, library]
date: 2018-03-25 10:34:56
---

# Introduction

Data structure defined in the **physical channels** headers. `struct` and `enum` only.

# Shortcuts

## phch

# Data Structures

## phch

Important part, physical channels.

### srslte\_cqi\_periodic\_cfg\_t

Location: `./lib/include/srslte/phy/phch/cqi.h`

```c++
typedef struct {
  bool     configured; 
  uint32_t pmi_idx; 
  uint32_t ri_idx;
  bool ri_idx_present;
  bool     simul_cqi_ack;
  bool     format_is_subband; 
  uint32_t subband_size; 
} srslte_cqi_periodic_cfg_t; 
```

Channel quality indicator message packing. Reference: 3GPP TS 36.212 version 10.0.0 Release 10 Sec. 5.2.2.6, 5.2.3.3.

### srslte\_cqi\_hl\_subband\_t

Location: `./lib/include/srslte/phy/phch/cqi.h`

```c++
typedef struct SRSLTE_API {
  uint8_t  wideband_cqi_cw0;      // 4-bit width
  uint32_t subband_diff_cqi_cw0;  // 2N-bit width
  uint8_t  wideband_cqi_cw1;      // if RI > 1 then 4-bit width otherwise 0-bit width
  uint32_t subband_diff_cqi_cw1;  // if RI > 1 then 2N-bit width otherwise 0-bit width
  uint32_t pmi;                   // if RI > 1 then 2-bit width otherwise 1-bit width
  uint32_t N;
  bool ri_present;
  bool pmi_present;
  bool four_antenna_ports;        // If cell has 4 antenna ports then true otherwise false
  bool rank_is_not_one;           // If rank > 1 then true otherwise false
} srslte_cqi_hl_subband_t;
```

### srslte\_cqi\_ue\_subband\_t

Location: `./lib/include/srslte/phy/phch/cqi.h`

```c++
typedef struct SRSLTE_API {
  uint8_t  wideband_cqi; // 4-bit width
  uint8_t  subband_diff_cqi; // 2-bit width
  uint32_t position_subband; // L-bit width
  uint32_t L;
} srslte_cqi_ue_subband_t;
```

### srslte\_cqi\_format2\_wideband\_t

Location: `./lib/include/srslte/phy/phch/cqi.h`

```c++
typedef struct SRSLTE_API {
  uint8_t  wideband_cqi; // 4-bit width
  uint8_t  spatial_diff_cqi; // If Rank==1 then it is 0-bit width otherwise it is 3-bit width
  uint8_t  pmi;
  bool pmi_present;
  bool four_antenna_ports;        // If cell has 4 antenna ports then true otherwise false
  bool rank_is_not_one;           // If rank > 1 then true otherwise false
} srslte_cqi_format2_wideband_t;
```

### srslte\_cqi\_format2\_subband\_t

Location: `./lib/include/srslte/phy/phch/cqi.h`

```c++
typedef struct SRSLTE_API {
  uint8_t  subband_cqi; // 4-bit width
  uint8_t  subband_label; // 1- or 2-bit width
  bool     subband_label_2_bits; // false, label=1-bit, true label=2-bits
} srslte_cqi_format2_subband_t;
```

### srslte\_cqi\_type\_t

Location: `./lib/include/srslte/phy/phch/cqi.h`

```c++
typedef enum {
  SRSLTE_CQI_TYPE_WIDEBAND = 0,
  SRSLTE_CQI_TYPE_SUBBAND,
  SRSLTE_CQI_TYPE_SUBBAND_UE,
  SRSLTE_CQI_TYPE_SUBBAND_HL
} srslte_cqi_type_t; 
```

### srslte\_cqi\_value\_t

Location: `./lib/include/srslte/phy/phch/cqi.h`

```c++
typedef struct {
  union {
    srslte_cqi_format2_wideband_t wideband;
    srslte_cqi_format2_subband_t  subband; 
    srslte_cqi_ue_subband_t       subband_ue;
    srslte_cqi_hl_subband_t       subband_hl;
  };
  srslte_cqi_type_t type; 
} srslte_cqi_value_t;
```

### srslte\_dci\_format\_t

Location: `./lib/include/srslte/phy/phch/dci.h`

```c++
typedef enum {
  SRSLTE_DCI_FORMAT0 = 0, 
  SRSLTE_DCI_FORMAT1, 
  SRSLTE_DCI_FORMAT1A, 
  SRSLTE_DCI_FORMAT1C, 
  SRSLTE_DCI_FORMAT1B,
  SRSLTE_DCI_FORMAT1D, 
  SRSLTE_DCI_FORMAT2, 
  SRSLTE_DCI_FORMAT2A, 
  SRSLTE_DCI_FORMAT2B, 
  //SRSLTE_DCI_FORMAT3, 
  //SRSLTE_DCI_FORMAT3A, 
  SRSLTE_DCI_NOF_FORMATS
} srslte_dci_format_t;
```

### srslte\_dci\_msg\_type\_t

Location: `./lib/include/srslte/phy/phch/dci.h`

```c++
typedef struct SRSLTE_API {
  enum {
    SRSLTE_DCI_MSG_TYPE_PUSCH_SCHED, 
    SRSLTE_DCI_MSG_TYPE_PDSCH_SCHED, 
    SRSLTE_DCI_MSG_TYPE_MCCH_CHANGE, 
    SRSLTE_DCI_MSG_TYPE_TPC_COMMAND, 
    SRSLTE_DCI_MSG_TYPE_RA_PROC_PDCCH
  } type;
  srslte_dci_format_t format;
}srslte_dci_msg_type_t;
```

Each type is for a different interface to packing/unpacking functions.

### dci\_spec\_t

Location: `./lib/include/srslte/phy/phch/dci.h`

```c++
typedef enum {
  SRSLTE_DCI_SPEC_COMMON_ = 0, 
  SRSLTE_DCI_SPEC_UE = 1
} dci_spec_t;
```

### srslte\_dci\_location\_t

Location: `./lib/include/srslte/phy/phch/dci.h`

```c++
typedef struct SRSLTE_API {
  uint32_t L;    // Aggregation level
  uint32_t ncce; // Position of first CCE of the dci
} srslte_dci_location_t;
```

### srslte\_dci\_msg\_t

Location: `./lib/include/srslte/phy/phch/dci.h`

```c++
typedef struct SRSLTE_API {
  uint8_t data[SRSLTE_DCI_MAX_BITS];
  uint32_t nof_bits;
  srslte_dci_format_t format; 
} srslte_dci_msg_t;
```

### srslte\_dci\_rar\_grant\_t

Location: `./lib/include/srslte/phy/phch/dci.h`

```c++
typedef struct SRSLTE_API {
  uint32_t rba;
  uint32_t trunc_mcs;
  uint32_t tpc_pusch;
  bool ul_delay;
  bool cqi_request; 
  bool hopping_flag; 
} srslte_dci_rar_grant_t;
```

### srslte\_pbch\_t

Location: `./lib/include/srslte/phy/phch/pbch.h`

```c++
typedef struct SRSLTE_API {
  srslte_cell_t cell;

  uint32_t nof_symbols;

  /* buffers */
  cf_t *ce[SRSLTE_MAX_PORTS];
  cf_t *symbols[SRSLTE_MAX_PORTS];
  cf_t *x[SRSLTE_MAX_PORTS];
  cf_t *d;
  float *llr;
  float *temp;
  float rm_f[SRSLTE_BCH_ENCODED_LEN];
  uint8_t *rm_b;
  uint8_t data[SRSLTE_BCH_PAYLOADCRC_LEN];
  uint8_t data_enc[SRSLTE_BCH_ENCODED_LEN];

  uint32_t frame_idx;

  /* tx & rx objects */
  srslte_modem_table_t mod;
  srslte_sequence_t seq;
  srslte_viterbi_t decoder;
  srslte_crc_t crc;
  srslte_convcoder_t encoder;
  bool search_all_ports;

} srslte_pbch_t;
```

### srslte\_pcfich\_t

Location: `./lib/include/srslte/phy/phch/pcfich.h`

```c++
typedef struct SRSLTE_API {
  srslte_cell_t cell;
  int nof_symbols;

  uint32_t nof_rx_antennas; 

  /* handler to REGs resource mapper */
  srslte_regs_t *regs;

  /* buffers */
  cf_t ce[SRSLTE_MAX_PORTS][SRSLTE_MAX_PORTS][PCFICH_RE];
  cf_t symbols[SRSLTE_MAX_PORTS][PCFICH_RE];
  cf_t x[SRSLTE_MAX_PORTS][PCFICH_RE];
  cf_t d[PCFICH_RE];

  // cfi table in floats 
  float cfi_table_float[3][PCFICH_CFI_LEN];

  /* bit message */
  uint8_t data[PCFICH_CFI_LEN];

  /* received soft bits */
  float data_f[PCFICH_CFI_LEN]; 

  /* tx & rx objects */
  srslte_modem_table_t mod;  
  srslte_sequence_t seq[SRSLTE_NSUBFRAMES_X_FRAME];

} srslte_pcfich_t;
```

### srslte\_pdcch\_search\_mode\_t

Location: `./lib/include/srslte/phy/phch/pdcch.h`

```c++
typedef enum SRSLTE_API {
  SEARCH_UE, SEARCH_COMMON
} srslte_pdcch_search_mode_t;
```

### srslte\_pdcch\_t

Location: `./lib/include/srslte/phy/phch/pdcch.h`

```c++
typedef struct SRSLTE_API {
  srslte_cell_t cell;
  uint32_t nof_regs[3];
  uint32_t nof_cce[3];
  uint32_t max_bits;
  uint32_t nof_rx_antennas;
  bool     is_ue;

  srslte_regs_t *regs;

  /* buffers */
  cf_t *ce[SRSLTE_MAX_PORTS][SRSLTE_MAX_PORTS];
  cf_t *symbols[SRSLTE_MAX_PORTS];
  cf_t *x[SRSLTE_MAX_PORTS];
  cf_t *d;
  uint8_t *e;
  float rm_f[3 * (SRSLTE_DCI_MAX_BITS + 16)];
  float *llr;

  /* tx & rx objects */
  srslte_modem_table_t mod;
  srslte_sequence_t seq[SRSLTE_NSUBFRAMES_X_FRAME];
  srslte_viterbi_t decoder;
  srslte_crc_t crc;

} srslte_pdcch_t;
```

### srslte\_pdsch\_user\_t

Location: `./lib/include/srslte/phy/phch/pdsch.h`

```c++
typedef struct {
  srslte_sequence_t seq[SRSLTE_MAX_CODEWORDS][SRSLTE_NSUBFRAMES_X_FRAME];
  uint32_t cell_id;
  bool sequence_generated;
} srslte_pdsch_user_t;
```

### srslte\_pdsch\_t

Location: `./lib/include/srslte/phy/phch/pdsch.h`

```c++
typedef struct SRSLTE_API {
  srslte_cell_t cell;

  uint32_t nof_rx_antennas;
  uint32_t last_nof_iterations[SRSLTE_MAX_CODEWORDS];

  uint32_t max_re;

  uint16_t ue_rnti;
  bool is_ue;

  /* Power allocation parameter 3GPP 36.213 Clause 5.2 Rho_b */
  float rho_a;

  /* buffers */
  // void buffers are shared for tx and rx
  cf_t *ce[SRSLTE_MAX_PORTS][SRSLTE_MAX_PORTS]; /* Channel estimation (Rx only) */
  cf_t *symbols[SRSLTE_MAX_PORTS];              /* PDSCH Encoded/Decoded Symbols */
  cf_t *x[SRSLTE_MAX_LAYERS];                   /* Layer mapped */
  cf_t *d[SRSLTE_MAX_CODEWORDS];                /* Modulated/Demodulated codewords */
  void *e[SRSLTE_MAX_CODEWORDS];

  /* tx & rx objects */
  srslte_modem_table_t mod[4];

  // This is to generate the scrambling seq for multiple CRNTIs
  srslte_pdsch_user_t **users;

  srslte_sequence_t tmp_seq;

  srslte_sch_t dl_sch;

} srslte_pdsch_t;
```

### srslte\_pdsch\_cfg\_t

Location: `./lib/include/srslte/phy/phch/pdsch_cfg.h`

```c++
typedef struct SRSLTE_API {
  srslte_cbsegm_t cb_segm[SRSLTE_MAX_CODEWORDS];
  srslte_ra_dl_grant_t grant;
  srslte_ra_nbits_t nbits[SRSLTE_MAX_CODEWORDS];
  uint32_t rv[SRSLTE_MAX_CODEWORDS];
  uint32_t sf_idx;
  uint32_t nof_layers;
  uint32_t codebook_idx;
  srslte_mimo_type_t mimo_type;
  bool tb_cw_swap;
} srslte_pdsch_cfg_t;
```

### srslte\_phich\_t

Location: `./lib/include/srslte/phy/phch/phich.h`

```c++
typedef struct SRSLTE_API {
  srslte_cell_t cell;

  uint32_t nof_rx_antennas; 

  /* handler to REGs resource mapper */
  srslte_regs_t *regs;

  /* buffers */
  cf_t ce[SRSLTE_MAX_PORTS][SRSLTE_MAX_PORTS][SRSLTE_PHICH_MAX_NSYMB];
  cf_t sf_symbols[SRSLTE_MAX_PORTS][SRSLTE_PHICH_MAX_NSYMB];
  cf_t x[SRSLTE_MAX_PORTS][SRSLTE_PHICH_MAX_NSYMB];
  cf_t d[SRSLTE_PHICH_MAX_NSYMB];
  cf_t d0[SRSLTE_PHICH_MAX_NSYMB];
  cf_t z[SRSLTE_PHICH_NBITS];

  /* bit message */
  uint8_t data[SRSLTE_PHICH_NBITS];
  float data_rx[SRSLTE_PHICH_NBITS];

  /* tx & rx objects */
  srslte_modem_table_t mod;
  srslte_sequence_t seq[SRSLTE_NSUBFRAMES_X_FRAME];

} srslte_phich_t;
```

### 

Location: `./lib/include/srslte/phy/phch/pmch.h`

```c++
typedef struct {
  srslte_sequence_t seq[SRSLTE_NSUBFRAMES_X_FRAME];  
} srslte_pmch_seq_t;
```

### srslte\_pmch\_cfg\_t

Location: `./lib/include/srslte/phy/phch/pmch.h`

```c++
typedef struct SRSLTE_API {
  srslte_cbsegm_t cb_segm;
  srslte_ra_dl_grant_t grant;
  srslte_ra_nbits_t nbits[SRSLTE_MAX_CODEWORDS];
  uint32_t sf_idx;
} srslte_pmch_cfg_t;
```

### srslte\_pmch\_t

Location: `./lib/include/srslte/phy/phch/pmch.h`

```c++
typedef struct SRSLTE_API {
  srslte_cell_t cell;

  uint32_t nof_rx_antennas;

  uint32_t max_re;

  /* buffers */
  // void buffers are shared for tx and rx
  cf_t *ce[SRSLTE_MAX_PORTS][SRSLTE_MAX_PORTS];
  cf_t *symbols[SRSLTE_MAX_PORTS];
  cf_t *x[SRSLTE_MAX_PORTS];
  cf_t *d;
  void *e;

  /* tx & rx objects */
  srslte_modem_table_t mod[4];

  // This is to generate the scrambling seq for multiple MBSFN Area IDs
  srslte_pmch_seq_t **seqs;

  srslte_sch_t dl_sch;

} srslte_pmch_t;
```

### srslte\_prach\_t

Location: `./lib/include/srslte/phy/phch/prach.h`

```c++
typedef struct SRSLTE_API {
  // Parameters from higher layers (extracted from SIB2)
  uint32_t config_idx; 
  uint32_t f;               // preamble format
  uint32_t rsi;             // rootSequenceIndex
  bool hs;                  // highSpeedFlag
  uint32_t zczc;            // zeroCorrelationZoneConfig
  uint32_t N_ifft_ul;       // IFFT size for uplink
  uint32_t N_ifft_prach;    // IFFT size for PRACH generation

  uint32_t max_N_ifft_ul;

  // Working parameters
  uint32_t N_zc;  // PRACH sequence length
  uint32_t N_cs;  // Cyclic shift size
  uint32_t N_seq; // Preamble length
  float    T_seq; // Preamble length in seconds
  float    T_tot; // Total sequence length in seconds
  uint32_t N_cp;  // Cyclic prefix length

  // Generated tables
  cf_t seqs[64][839];         // Our set of 64 preamble sequences
  cf_t dft_seqs[64][839];     // DFT-precoded seqs
  uint32_t root_seqs_idx[64]; // Indices of root seqs in seqs table
  uint32_t N_roots;           // Number of root sequences used in this configuration

  // Containers
  cf_t *ifft_in;
  cf_t *ifft_out;
  cf_t *prach_bins;
  cf_t *corr_spec;
  float *corr;

  // PRACH IFFT
  srslte_dft_plan_t fft;
  srslte_dft_plan_t ifft;

  // ZC-sequence FFT and IFFT
  srslte_dft_plan_t zc_fft;
  srslte_dft_plan_t zc_ifft;

  cf_t *signal_fft; 
  float detect_factor; 

  uint32_t deadzone; 
  float    peak_values[65];
  uint32_t peak_offsets[65];

} srslte_prach_t;
```

### srslte\_prach\_sf\_config\_t

Location: `./lib/include/srslte/phy/phch/prach.h`

```c++
typedef struct SRSLTE_API {
  int nof_sf;
  uint32_t sf[5];
} srslte_prach_sf_config_t;
```

### srslte\_prach\_sfn\_t

Location: `./lib/include/srslte/phy/phch/prach.h`

```c++
typedef enum SRSLTE_API {
  SRSLTE_PRACH_SFN_EVEN = 0,
  SRSLTE_PRACH_SFN_ANY,  
} srslte_prach_sfn_t;
```

### srslte\_prach\_cfg\_t

Location: `./lib/include/srslte/phy/phch/prach.h`

```c++
typedef struct {
  uint32_t config_idx;
  uint32_t root_seq_idx;
  uint32_t zero_corr_zone;
  uint32_t freq_offset;
  bool     hs_flag; 
} srslte_prach_cfg_t;
```

### 

Location: `./lib/include/srslte/phy/phch/pucch.h`

```c++
typedef enum SRSLTE_API {
  SRSLTE_PUCCH_FORMAT_1 = 0, 
  SRSLTE_PUCCH_FORMAT_1A, 
  SRSLTE_PUCCH_FORMAT_1B, 
  SRSLTE_PUCCH_FORMAT_2, 
  SRSLTE_PUCCH_FORMAT_2A, 
  SRSLTE_PUCCH_FORMAT_2B,
  SRSLTE_PUCCH_FORMAT_ERROR,
} srslte_pucch_format_t; 
```

### srslte\_pucch\_sched\_t

Location: `./lib/include/srslte/phy/phch/pucch.h`

```c++
typedef struct SRSLTE_API {
  bool sps_enabled; 
  uint32_t tpc_for_pucch; 
  uint32_t N_pucch_1; 
  uint32_t n_pucch_1[4]; // 4 n_pucch resources specified by RRC  
  uint32_t n_pucch_2; 
  uint32_t n_pucch_sr; 
}srslte_pucch_sched_t;
```

### srslte\_pucch\_cfg\_t

Location: `./lib/include/srslte/phy/phch/pucch.h`

```c++
typedef struct SRSLTE_API {
  // Common configuration 
  uint32_t delta_pucch_shift; 
  uint32_t n_rb_2; 
  uint32_t N_cs; 
  uint32_t n1_pucch_an; 

  // SRS configuration 
  bool srs_configured; 
  uint32_t srs_cs_subf_cfg;
  bool srs_simul_ack; 
} srslte_pucch_cfg_t;
```

### srslte\_pucch\_user\_t

Location: `./lib/include/srslte/phy/phch/pucch.h`

```c++
typedef struct  {
  srslte_sequence_t seq_f2[SRSLTE_NSUBFRAMES_X_FRAME];
  bool sequence_generated;
} srslte_pucch_user_t;
```

### srslte\_pucch\_t

Location: `./lib/include/srslte/phy/phch/pucch.h`

```c++
typedef struct SRSLTE_API {
  srslte_cell_t cell;
  srslte_pucch_cfg_t pucch_cfg;
  srslte_modem_table_t mod; 

  srslte_uci_cqi_pucch_t cqi; 

  srslte_pucch_user_t **users;

  uint8_t bits_scram[SRSLTE_PUCCH_MAX_BITS];
  cf_t d[SRSLTE_PUCCH_MAX_BITS/2];
  uint32_t n_cs_cell[SRSLTE_NSLOTS_X_FRAME][SRSLTE_CP_NORM_NSYMB]; 
  uint32_t f_gh[SRSLTE_NSLOTS_X_FRAME];
  float tmp_arg[SRSLTE_PUCCH_N_SEQ];

  cf_t *z;
  cf_t *z_tmp;
  cf_t *ce;

  bool shortened; 
  bool group_hopping_en;

  float threshold_format1;
  float last_corr;
  uint32_t last_n_prb;
  uint32_t last_n_pucch;

}srslte_pucch_t;
```

### srslte\_pusch\_hopping\_cfg\_t

Location: `./lib/include/srslte/phy/phch/pusch.h`

```c++
typedef struct {
  enum {
    SRSLTE_PUSCH_HOP_MODE_INTER_SF = 1,
    SRSLTE_PUSCH_HOP_MODE_INTRA_SF = 0
  } hop_mode; 
  uint32_t hopping_offset;
  uint32_t n_sb;
} srslte_pusch_hopping_cfg_t;
```

### srslte\_pusch\_user\_t

Location: `./lib/include/srslte/phy/phch/pusch.h`

```c++
typedef struct {
  srslte_sequence_t seq[SRSLTE_NSUBFRAMES_X_FRAME];
  uint32_t cell_id;
  bool sequence_generated;
} srslte_pusch_user_t;
```

### srslte\_pusch\_t

Location: `./lib/include/srslte/phy/phch/pusch.h`

```c++
typedef struct SRSLTE_API {
  srslte_cell_t cell;

  bool is_ue;
  uint16_t ue_rnti;
  uint32_t max_re;

  srslte_dft_precoding_t dft_precoding;  

  /* buffers */
  // void buffers are shared for tx and rx
  cf_t *ce;
  cf_t *z;
  cf_t *d;

  void *q;
  void *g;

  /* tx & rx objects */
  srslte_modem_table_t mod[4];
  srslte_sequence_t seq_type2_fo; 

  // This is to generate the scrambling seq for multiple CRNTIs
  srslte_pusch_user_t **users;
  srslte_sequence_t tmp_seq;

  srslte_sch_t ul_sch;
  bool shortened;

}srslte_pusch_t;
```

### srslte\_uci\_cfg\_t

Location: `./lib/include/srslte/phy/phch/pusch_cfg.h`

```c++
typedef struct SRSLTE_API {
  uint32_t I_offset_cqi;
  uint32_t I_offset_ri;
  uint32_t I_offset_ack;
} srslte_uci_cfg_t;
```

### srslte\_pusch\_cfg\_t

Location: `./lib/include/srslte/phy/phch/pusch_cfg.h`

```c++
typedef struct SRSLTE_API {
  srslte_cbsegm_t cb_segm; 
  srslte_ra_ul_grant_t grant; 
  srslte_ra_nbits_t nbits; 
  srslte_uci_cfg_t uci_cfg; 
  uint32_t rv; 
  uint32_t sf_idx;
  uint32_t tti; 
  srslte_cp_t cp; 
  uint32_t last_O_cqi;
} srslte_pusch_cfg_t;
```

### srslte\_ra\_mcs\_t

Location: `./lib/include/srslte/phy/phch/ra.h`

```c++
typedef struct SRSLTE_API {
  srslte_mod_t mod;
  int tbs;
  uint32_t idx; 
} srslte_ra_mcs_t;
```

### srslte\_ra\_nbits\_t

Location: `./lib/include/srslte/phy/phch/ra.h`

```c++
typedef struct {
  uint32_t lstart; 
  uint32_t nof_symb; 
  uint32_t nof_bits;
  uint32_t nof_re; 
} srslte_ra_nbits_t;
```

Structure that gives the number of encoded bits and RE for a UL/DL grant.

### srslte\_ra\_type\_t

Location: `./lib/include/srslte/phy/phch/ra.h`

```c++
typedef enum SRSLTE_API {
  SRSLTE_RA_ALLOC_TYPE0 = 0, 
  SRSLTE_RA_ALLOC_TYPE1 = 1, 
  SRSLTE_RA_ALLOC_TYPE2 = 2
} srslte_ra_type_t;
```

### srslte\_ra\_type0\_t

Location: `./lib/include/srslte/phy/phch/ra.h`

```c++
typedef struct SRSLTE_API {
  uint32_t rbg_bitmask;
} srslte_ra_type0_t;
```

### srslte\_ra\_type1\_t

Location: `./lib/include/srslte/phy/phch/ra.h`

```c++
typedef struct SRSLTE_API {
  uint32_t vrb_bitmask;
  uint32_t rbg_subset;
  bool shift;
} srslte_ra_type1_t;
```

### srslte\_ra\_type2\_t

Location: `./lib/include/srslte/phy/phch/ra.h`

```c++
typedef struct SRSLTE_API {
  uint32_t riv; // if L_crb==0, DCI message packer will take this value directly
  uint32_t L_crb;
  uint32_t RB_start;
  enum {
    SRSLTE_RA_TYPE2_NPRB1A_2 = 0, SRSLTE_RA_TYPE2_NPRB1A_3 = 1
  } n_prb1a;
  enum {
    SRSLTE_RA_TYPE2_NG1 = 0, SRSLTE_RA_TYPE2_NG2 = 1
  } n_gap;
  enum {
    SRSLTE_RA_TYPE2_LOC = 0, SRSLTE_RA_TYPE2_DIST = 1
  } mode;
} srslte_ra_type2_t;
```

### srslte\_ra\_dl\_grant\_t

Location: `./lib/include/srslte/phy/phch/ra.h`

```c++
typedef struct SRSLTE_API {
  bool prb_idx[2][SRSLTE_MAX_PRB];
  uint32_t nof_prb;  
  uint32_t Qm[SRSLTE_MAX_CODEWORDS];
  srslte_ra_mcs_t mcs[SRSLTE_MAX_CODEWORDS];
  srslte_sf_t sf_type;
  bool tb_en[SRSLTE_MAX_CODEWORDS];
  uint32_t pinfo;
  bool tb_cw_swap;
} srslte_ra_dl_grant_t;
```

Structures used for downlink resource allocation.

### srslte\_ra\_dl\_dci\_t

Location: `./lib/include/srslte/phy/phch/ra.h`

```c++
typedef struct SRSLTE_API {

  srslte_ra_type_t alloc_type;
  union {
    srslte_ra_type0_t type0_alloc;
    srslte_ra_type1_t type1_alloc;
    srslte_ra_type2_t type2_alloc;
  };

  uint32_t harq_process;
  uint32_t mcs_idx;
  int      rv_idx;
  bool     ndi;
  uint32_t mcs_idx_1;
  int      rv_idx_1;
  bool     ndi_1;

  bool     tb_cw_swap; 
  bool     sram_id; 
  uint8_t  pinfo; 
  bool     pconf;
  bool     power_offset; 

  uint8_t tpc_pucch;

  bool     tb_en[2]; 

  bool     is_ra_order;
  uint32_t ra_preamble;
  uint32_t ra_mask_idx;

  bool     dci_is_1a;
  bool     dci_is_1c; 
} srslte_ra_dl_dci_t;
```

Unpacked DCI message for DL grant.

### srslte\_ra\_ul\_grant\_t

Location: `./lib/include/srslte/phy/phch/ra.h`

```c++
typedef struct SRSLTE_API {
  uint32_t n_prb[2];
  uint32_t n_prb_tilde[2];
  uint32_t L_prb;
  uint32_t freq_hopping; 
  uint32_t M_sc; 
  uint32_t M_sc_init; 
  uint32_t Qm; 
  srslte_ra_mcs_t mcs;
  uint32_t ncs_dmrs;
} srslte_ra_ul_grant_t;
```

Structures used for uplink resource allocation.

### srslte\_ra\_ul\_dci\_t

Location: `./lib/include/srslte/phy/phch/ra.h`

```c++
typedef struct SRSLTE_API {
  /* 36.213 Table 8.4-2: SRSLTE_RA_PUSCH_HOP_HALF is 0 for < 10 Mhz and 10 for > 10 Mhz.
   * SRSLTE_RA_PUSCH_HOP_QUART is 00 for > 10 Mhz and SRSLTE_RA_PUSCH_HOP_QUART_NEG is 01 for > 10 Mhz.
   */
  enum {
    SRSLTE_RA_PUSCH_HOP_DISABLED = -1,
    SRSLTE_RA_PUSCH_HOP_QUART = 0,
    SRSLTE_RA_PUSCH_HOP_QUART_NEG = 1,
    SRSLTE_RA_PUSCH_HOP_HALF = 2,
    SRSLTE_RA_PUSCH_HOP_TYPE2 = 3
  } freq_hop_fl;

  srslte_ra_ul_grant_t prb_alloc;

  srslte_ra_type2_t type2_alloc;
  uint32_t mcs_idx;
  uint32_t rv_idx;   
  uint32_t n_dmrs; 
  bool ndi;
  bool cqi_request;
  uint8_t tpc_pusch;

} srslte_ra_ul_dci_t;
```

Unpacked DCI Format0 message.

### srslte\_phy\_grant\_t

Location: `./lib/include/srslte/phy/phch/ra.h`

```c++
typedef union {
  srslte_ra_ul_grant_t ul;
  srslte_ra_dl_grant_t dl;
} srslte_phy_grant_t;
```

### srslte\_regs\_reg\_t

Location: `./lib/include/srslte/phy/phch/regs.h`

```c++
typedef struct SRSLTE_API {
  uint32_t k[4];
  uint32_t k0;
  uint32_t l;
  bool assigned;
}srslte_regs_reg_t;
```

### srslte\_regs\_ch\_t

Location: `./lib/include/srslte/phy/phch/regs.h`

```c++
typedef struct SRSLTE_API {
  uint32_t nof_regs;
  srslte_regs_reg_t **regs;
}srslte_regs_ch_t;
```

### srslte\_regs\_t

Location: `./lib/include/srslte/phy/phch/regs.h`

```c++
typedef struct SRSLTE_API {
  srslte_cell_t cell;
  uint32_t max_ctrl_symbols;
  uint32_t ngroups_phich;

  srslte_phich_resources_t phich_res;
  srslte_phich_length_t phich_len;

  srslte_regs_ch_t pcfich;
  srslte_regs_ch_t *phich; // there are several phich
  srslte_regs_ch_t pdcch[3]; /* PDCCH indexing, permutation and interleaving is computed for
            the three possible CFI value */

  uint32_t nof_regs;
  srslte_regs_reg_t *regs;
}srslte_regs_t;
```

### srslte\_sch\_t

Location: `./lib/include/srslte/phy/phch/sch.h`

```c++
typedef struct SRSLTE_API {

  uint32_t max_iterations;
  uint32_t nof_iterations;

  /* buffers */
  uint8_t *cb_in; 
  uint8_t *parity_bits;  
  void *e;
  uint8_t *temp_g_bits;
  uint16_t *ul_interleaver;
  srslte_uci_bit_t ack_ri_bits[12*288];
  uint32_t nof_ri_ack_bits; 

  srslte_tcod_t encoder;
  srslte_tdec_t decoder;  
  srslte_crc_t crc_tb;
  srslte_crc_t crc_cb;

  srslte_uci_cqi_pusch_t uci_cqi;

} srslte_sch_t;
```

DL-SCH AND UL-SCH common functions.

### srslte\_uci\_cqi\_pusch\_t

Location: `./lib/include/srslte/phy/phch/uci.h`

```c++
typedef struct SRSLTE_API {
  srslte_crc_t crc;
  srslte_viterbi_t viterbi; 
  uint8_t tmp_cqi[SRSLTE_UCI_MAX_CQI_LEN_PUSCH];
  uint8_t encoded_cqi[3*SRSLTE_UCI_MAX_CQI_LEN_PUSCH];
  int16_t encoded_cqi_s[3*SRSLTE_UCI_MAX_CQI_LEN_PUSCH];
  uint8_t *cqi_table[11];
  int16_t *cqi_table_s[11];
} srslte_uci_cqi_pusch_t;
```

### srslte\_uci\_cqi\_pucch\_t

Location: `./lib/include/srslte/phy/phch/uci.h`

```c++
typedef struct SRSLTE_API {
  uint8_t **cqi_table;
  int16_t **cqi_table_s;
} srslte_uci_cqi_pucch_t;
```

### srslte\_uci\_data\_t

Location: `./lib/include/srslte/phy/phch/uci.h`

```c++
typedef struct SRSLTE_API {
  uint8_t  uci_cqi[SRSLTE_CQI_MAX_BITS];
  uint32_t uci_cqi_len;
  uint8_t  uci_ri;  // Only 1-bit supported for RI
  uint32_t uci_ri_len;
  uint8_t  uci_ack;   // 1st codeword bit for HARQ-ACK
  uint8_t  uci_ack_2; // 2st codeword bit for HARQ-ACK
  uint32_t uci_ack_len;
  bool ri_periodic_report;
  bool scheduling_request; 
  bool channel_selection; 
  bool cqi_ack; 
} srslte_uci_data_t;
```

### srslte\_uci\_bit\_type\_t

Location: `./lib/include/srslte/phy/phch/uci.h`

```c++
typedef enum {
  UCI_BIT_1 = 0, UCI_BIT_0, UCI_BIT_REPETITION, UCI_BIT_PLACEHOLDER
} srslte_uci_bit_type_t;
```

### srslte\_uci\_bit\_t

Location: `./lib/include/srslte/phy/phch/uci.h`

```c++
typedef struct {
  uint32_t position;
  srslte_uci_bit_type_t type;
} srslte_uci_bit_t;
```
