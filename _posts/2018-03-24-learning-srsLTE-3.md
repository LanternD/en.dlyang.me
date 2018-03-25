---
layout: post
title: Learning srsLTE - 3
description: srsLTE data structure overview and references. Physical layer data structure only.
permalink: /learning-srslte-3/
categories: [blog]
tags: [srslte, software radio, software, library]
date: 2018-03-24 17:34:56
---

# Introduction

Data structure defined in the physical layer headers. `struct` and `enum` only. No **Physical channels** data structure! See post [Learning srsLTE - 4](../learning-srslte-4/) for that part.

# Shortcuts

## agc

## ch\_estimation

## common

## dft

## enb

## fec

## io

## modem

## resampling

## rf

## sync

## ue

## utils

# Data Structures

## agc

Automatic gain control.

### srslte\_agc\_mode\_t

Location: `./lib/include/srslte/phy/agc/agc.h`

```c++
typedef enum SRSLTE_API {
  SRSLTE_AGC_MODE_ENERGY = 0, 
  SRSLTE_AGC_MODE_PEAK_AMPLITUDE  
} srslte_agc_mode_t;
```

### srslte\_agc\_t

Location: `./lib/include/srslte/phy/agc/agc.h`

```c++
typedef struct SRSLTE_API{
  float bandwidth;
  double gain; 
  float y_out;
  bool lock;
  bool isfirst; 
  void *uhd_handler; 
  double (*set_gain_callback) (void*,double);
  srslte_agc_mode_t mode; 
  float target;
  uint32_t nof_frames; 
  uint32_t frame_cnt; 
  float *y_tmp;
} srslte_agc_t;
```

## ch\_estimation

Channel estimation.

### srslte\_chest\_dl\_noise\_alg\_t

Location: `./lib/include/srslte/phy/ch_estimation/chest_dl.h`

```c++
typedef enum {
  SRSLTE_NOISE_ALG_REFS, 
  SRSLTE_NOISE_ALG_PSS, 
  SRSLTE_NOISE_ALG_EMPTY,
} srslte_chest_dl_noise_alg_t;
```

### srslte\_chest\_dl\_t

Location: `./lib/include/srslte/phy/ch_estimation/chest_dl.h`

```c++
typedef struct {
  srslte_cell_t cell; 
  srslte_refsignal_t   csr_refs;
  srslte_refsignal_t **mbsfn_refs;


  cf_t *pilot_estimates;
  cf_t *pilot_estimates_average; 
  cf_t *pilot_recv_signal; 
  cf_t *tmp_noise; 
  cf_t *tmp_cfo_estimate;

#ifdef FREQ_SEL_SNR  
  float snr_vector[12000];
  float pilot_power[12000];
#endif
  uint32_t smooth_filter_len; 
  float smooth_filter[SRSLTE_CHEST_MAX_SMOOTH_FIL_LEN];

  srslte_interp_linsrslte_vec_t srslte_interp_linvec; 
  srslte_interp_lin_t srslte_interp_lin; 
  srslte_interp_lin_t srslte_interp_lin_3;
  srslte_interp_lin_t srslte_interp_lin_mbsfn;
  float rssi[SRSLTE_MAX_PORTS][SRSLTE_MAX_PORTS]; 
  float rsrp[SRSLTE_MAX_PORTS][SRSLTE_MAX_PORTS]; 
  float noise_estimate[SRSLTE_MAX_PORTS][SRSLTE_MAX_PORTS];
  float cfo;

  bool     cfo_estimate_enable;
  uint32_t cfo_estimate_sf_mask;

  /* Use PSS for noise estimation in LS linear interpolation mode */
  cf_t pss_signal[SRSLTE_PSS_LEN];
  cf_t tmp_pss[SRSLTE_PSS_LEN];
  cf_t tmp_pss_noisy[SRSLTE_PSS_LEN];

  srslte_chest_dl_noise_alg_t noise_alg; 
  int last_nof_antennas;

  bool average_subframe;
} srslte_chest_dl_t;
```

### srslte\_chest\_ul\_t

Location: `./lib/include/srslte/phy/ch_estimation/chest_ul.h`

```c++
typedef struct {
  srslte_cell_t cell; 

  srslte_refsignal_ul_t             dmrs_signal;
  srslte_refsignal_ul_dmrs_pregen_t dmrs_pregen; 
  bool dmrs_signal_configured; 

  cf_t *pilot_estimates;
  cf_t *pilot_estimates_tmp[4];
  cf_t *pilot_recv_signal; 
  cf_t *pilot_known_signal; 
  cf_t *tmp_noise; 

#ifdef FREQ_SEL_SNR  
  float snr_vector[12000];
  float pilot_power[12000];
#endif
  uint32_t smooth_filter_len; 
  float smooth_filter[SRSLTE_CHEST_MAX_SMOOTH_FIL_LEN];

  srslte_interp_linsrslte_vec_t srslte_interp_linvec; 

  float pilot_power; 
  float noise_estimate;

} srslte_chest_ul_t;
```

### srslte\_refsignal\_t

Cell-specific reference signal (CRS).

Location: `./lib/include/srslte/phy/ch_estimation/refsignal_dl.h`

```c++
typedef struct SRSLTE_API {
  srslte_cell_t cell; 
  cf_t         *pilots[2][SRSLTE_NSUBFRAMES_X_FRAME]; // Saves the reference signal per subframe for ports 0,1 and ports 2,3
  srslte_sf_t   type;
  uint16_t      mbsfn_area_id;
} srslte_refsignal_t;
```

### srslte\_refsignal\_dmrs\_pusch\_cfg\_t

Location: `./lib/include/srslte/phy/ch_estimation/refsignal_ul.h`

```c++
typedef struct SRSLTE_API {
  uint32_t cyclic_shift; 
  uint32_t delta_ss;  
  bool group_hopping_en; 
  bool sequence_hopping_en; 
}srslte_refsignal_dmrs_pusch_cfg_t;
```

PUSCH DMRS common configuration (received in SIB2).

### srslte\_refsignal\_srs\_cfg\_t

Location: `./lib/include/srslte/phy/ch_estimation/refsignal_ul.h`

```c++
typedef struct SRSLTE_API {
  // Common Configuration 
  uint32_t subframe_config;
  uint32_t bw_cfg; 

  // Dedicated configuration 
  uint32_t B; 
  uint32_t b_hop; 
  uint32_t n_srs; 
  uint32_t I_srs; 
  uint32_t k_tc; 
  uint32_t n_rrc;
  bool configured; 
}srslte_refsignal_srs_cfg_t;
```

### srslte\_refsignal\_ul\_t

Location: `./lib/include/srslte/phy/ch_estimation/refsignal_ul.h`

```c++
typedef struct SRSLTE_API {
  srslte_cell_t cell; 
  srslte_refsignal_dmrs_pusch_cfg_t pusch_cfg; 
  srslte_pucch_cfg_t pucch_cfg; 
  srslte_refsignal_srs_cfg_t srs_cfg; 

  uint32_t n_cs_cell[SRSLTE_NSLOTS_X_FRAME][SRSLTE_CP_NORM_NSYMB]; 
  float *tmp_arg; 
  uint32_t n_prs_pusch[SRSLTE_NOF_DELTA_SS][SRSLTE_NSLOTS_X_FRAME]; // We precompute n_prs needed for cyclic shift alpha at srslte_refsignal_dl_init()
  uint32_t f_gh[SRSLTE_NSLOTS_X_FRAME];
  uint32_t u_pucch[SRSLTE_NSLOTS_X_FRAME];
  uint32_t v_pusch[SRSLTE_NSLOTS_X_FRAME][SRSLTE_NOF_DELTA_SS];
} srslte_refsignal_ul_t;
```

Uplink DeModulation Reference Signal (DMRS).

### srslte\_refsignal\_ul\_dmrs\_pregen\_t

Location: `./lib/include/srslte/phy/ch_estimation/refsignal_ul.h`

```c++
typedef struct {
  cf_t **r[SRSLTE_NOF_CSHIFT][SRSLTE_NSUBFRAMES_X_FRAME]; 
} srslte_refsignal_ul_dmrs_pregen_t;
```

### srslte\_refsignal\_srs\_pregen\_t

Location: `./lib/include/srslte/phy/ch_estimation/refsignal_ul.h`

```c++
typedef struct {
  cf_t *r[SRSLTE_NSUBFRAMES_X_FRAME]; 
} srslte_refsignal_srs_pregen_t;
```

## common

Commonly used API data structure.

### srslte\_phich\_length\_t

Location: `./lib/include/srslte/phy/common/phy_common.h`

```c++
typedef enum SRSLTE_API { 
  SRSLTE_PHICH_NORM = 0, 
  SRSLTE_PHICH_EXT  
} srslte_phich_length_t;
```

### srslte\_phich\_resources\_t

Location: `./lib/include/srslte/phy/common/phy_common.h`

```c++
typedef enum SRSLTE_API { 
  SRSLTE_PHICH_R_1_6 = 0, 
  SRSLTE_PHICH_R_1_2, 
  SRSLTE_PHICH_R_1, 
  SRSLTE_PHICH_R_2

} srslte_phich_resources_t;
```

### srslte\_rnti\_type\_t

Location: `./lib/include/srslte/phy/common/phy_common.h`

```c++
typedef enum {
  SRSLTE_RNTI_USER = 0, /* Cell RNTI */
  SRSLTE_RNTI_SI,       /* System Information RNTI */
  SRSLTE_RNTI_RAR,      /* Random Access RNTI */
  SRSLTE_RNTI_TEMP,     /* Temporary C-RNTI */
  SRSLTE_RNTI_SPS,      /* Semi-Persistent Scheduling C-RNTI */
  SRSLTE_RNTI_PCH,      /* Paging RNTI */
  SRSLTE_RNTI_MBSFN,
  SRSLTE_RNTI_NOF_TYPES
} srslte_rnti_type_t;
```

### srslte\_cell\_t

Location: `./lib/include/srslte/phy/common/phy_common.h`

```c++
typedef struct SRSLTE_API {
  uint32_t nof_prb;
  uint32_t nof_ports; 
  uint32_t id;
  srslte_cp_t cp;
  srslte_phich_length_t phich_length;
  srslte_phich_resources_t phich_resources;
}srslte_cell_t;
```

### srslte\_mimo\_type\_t

Location: `./lib/include/srslte/phy/common/phy_common.h`

```c++
typedef enum SRSLTE_API {
  SRSLTE_MIMO_TYPE_SINGLE_ANTENNA,
  SRSLTE_MIMO_TYPE_TX_DIVERSITY, 
  SRSLTE_MIMO_TYPE_SPATIAL_MULTIPLEX, 
  SRSLTE_MIMO_TYPE_CDD
} srslte_mimo_type_t;
```

### srslte\_mimo\_decoder\_t

Location: `./lib/include/srslte/phy/common/phy_common.h`

```c++
typedef enum SRSLTE_API {
  SRSLTE_MIMO_DECODER_ZF,
  SRSLTE_MIMO_DECODER_MMSE
} srslte_mimo_decoder_t;
```

### srslte\_mod\_t

Location: `./lib/include/srslte/phy/common/phy_common.h`

```c++
typedef enum SRSLTE_API {
  SRSLTE_MOD_BPSK = 0, 
  SRSLTE_MOD_QPSK, 
  SRSLTE_MOD_16QAM, 
  SRSLTE_MOD_64QAM,
  SRSLTE_MOD_LAST
} srslte_mod_t;
```

### srslte\_earfcn\_t

Location: `./lib/include/srslte/phy/common/phy_common.h`

```c++
typedef struct SRSLTE_API {
  int id;
  float fd;
} srslte_earfcn_t;
```

### band\_geographical\_area

Location: `./lib/include/srslte/phy/common/phy_common.h`

```c++
enum band_geographical_area {
  SRSLTE_BAND_GEO_AREA_ALL, 
  SRSLTE_BAND_GEO_AREA_NAR, 
  SRSLTE_BAND_GEO_AREA_APAC, 
  SRSLTE_BAND_GEO_AREA_EMEA, 
  SRSLTE_BAND_GEO_AREA_JAPAN, 
  SRSLTE_BAND_GEO_AREA_CALA, 
  SRSLTE_BAND_GEO_AREA_NA
};
```

### phy\_logger\_level\_t

Location: `./lib/include/srslte/phy/common/phy_logger.h`

```c++
typedef enum {LOG_LEVEL_INFO, LOG_LEVEL_DEBUG, LOG_LEVEL_ERROR} phy_logger_level_t;
```

### srslte\_sequence\_t

Location: `./lib/include/srslte/phy/common/sequence.h`

```c++
typedef struct SRSLTE_API {
  uint8_t *c;
  uint8_t *c_bytes;
  float *c_float;
  short *c_short;
  uint32_t cur_len;
  uint32_t max_len;
} srslte_sequence_t;
```

### srslte\_timestamp\_t

Location: `./lib/include/srslte/phy/common/timestamp.h`

```c++
typedef struct SRSLTE_API{
  time_t full_secs;
  double frac_secs;
}srslte_timestamp_t;
```

This one is frequently used.

## dft

Discrete Fourier transformation.

### srslte\_dft\_mode\_t

Location: `./lib/include/srslte/phy/dft/dft.h`

```c++
typedef enum {
  SRSLTE_DFT_COMPLEX, SRSLTE_REAL
}srslte_dft_mode_t;
```

### srslte\_dft\_dir\_t

Location: `./lib/include/srslte/phy/dft/dft.h`

```c++
typedef enum {
  SRSLTE_DFT_FORWARD, SRSLTE_DFT_BACKWARD
}srslte_dft_dir_t;
```

### srslte\_dft\_plan\_t

Location: `./lib/include/srslte/phy/dft/dft.h`

```c++
typedef struct SRSLTE_API {
  int init_size;      // DFT length used in the first initialization
  int size;           // DFT length
  void *in;           // Input buffer
  void *out;          // Output buffer
  void *p;            // DFT plan
  bool is_guru;
  bool forward;       // Forward transform?
  bool mirror;        // Shift negative and positive frequencies?
  bool db;            // Provide output in dB?
  bool norm;          // Normalize output?
  bool dc;            // Handle insertion/removal of null DC carrier internally?
  srslte_dft_dir_t dir;     // Forward/Backward
  srslte_dft_mode_t mode;   // Complex/Real
}srslte_dft_plan_t;
```

### srslte\_dft\_precoding\_t

Location: `./lib/include/srslte/phy/dft/dft_precoding.h`

```c++
typedef struct SRSLTE_API {

  uint32_t max_prb;  
  srslte_dft_plan_t dft_plan[SRSLTE_MAX_PRB+1];

}srslte_dft_precoding_t;
```

DFT-based Transform Precoding object.

### srslte\_ofdm\_t

Location: `./lib/include/srslte/phy/dft/ofdm.h`

```c++
typedef struct SRSLTE_API{
  srslte_dft_plan_t fft_plan;
  srslte_dft_plan_t fft_plan_sf[2];
  uint32_t max_prb;
  uint32_t nof_symbols;
  uint32_t symbol_sz;
  uint32_t nof_guards;
  uint32_t nof_re;
  uint32_t slot_sz;
  uint32_t sf_sz;
  srslte_cp_t cp;
  cf_t *tmp; // for removing zero padding
  cf_t *in_buffer;
  cf_t *out_buffer;

  bool     mbsfn_subframe;
  uint32_t mbsfn_guard_len;
  uint32_t nof_symbols_mbsfn;
  uint8_t  non_mbsfn_region;


  bool freq_shift;
  float freq_shift_f;
  cf_t *shift_buffer; 
}srslte_ofdm_t;
```

This is common for both directions.

## enb

eNodeB.

### srslte\_enb\_dl\_t

Location: `./lib/include/srslte/phy/enb/enb_dl.h`

```c++
typedef struct SRSLTE_API {
  srslte_cell_t cell;

  cf_t *sf_symbols[SRSLTE_MAX_PORTS]; 
  cf_t *slot1_symbols[SRSLTE_MAX_PORTS];

  srslte_ofdm_t   ifft[SRSLTE_MAX_PORTS];
  srslte_pbch_t   pbch;
  srslte_pcfich_t pcfich;
  srslte_regs_t   regs;
  srslte_pdcch_t  pdcch;
  srslte_pdsch_t  pdsch;
  srslte_phich_t  phich; 

  srslte_refsignal_t csr_signal;
  srslte_pdsch_cfg_t pdsch_cfg; 
  srslte_ra_dl_dci_t dl_dci;

  srslte_dci_format_t dci_format;
  uint32_t cfi;

  cf_t pss_signal[SRSLTE_PSS_LEN];
  float sss_signal0[SRSLTE_SSS_LEN]; 
  float sss_signal5[SRSLTE_SSS_LEN]; 

  float tx_amp;
  float rho_b;

  uint8_t tmp[1024*128];

} srslte_enb_dl_t;
```

### srslte\_enb\_dl\_pdsch\_t

Location: `./lib/include/srslte/phy/enb/enb_dl.h`

```c++
typedef struct {
  uint16_t                rnti; 
  srslte_dci_format_t     dci_format;
  srslte_ra_dl_dci_t      grant;
  srslte_dci_location_t   location; 
  srslte_softbuffer_tx_t *softbuffers[SRSLTE_MAX_TB];
  uint8_t                *data[SRSLTE_MAX_TB];
} srslte_enb_dl_pdsch_t;
```

### srslte\_enb\_dl\_phich\_t

Location: `./lib/include/srslte/phy/enb/enb_dl.h`

```c++
typedef struct {
  uint16_t rnti; 
  uint8_t  ack;
  uint32_t n_prb_lowest;
  uint32_t n_dmrs;  
} srslte_enb_dl_phich_t;
```

### srslte\_enb\_ul\_phich\_info\_t

Location: `./lib/include/srslte/phy/enb/enb_ul.h`

```c++
typedef struct {
  uint32_t n_prb_lowest;
  uint32_t n_dmrs;  
} srslte_enb_ul_phich_info_t;
```

### srslte\_enb\_ul\_user\_t

Location: `./lib/include/srslte/phy/enb/enb_ul.h`

```c++
typedef struct {
  bool uci_cfg_en;
  bool srs_cfg_en;
  srslte_uci_cfg_t uci_cfg;
  srslte_refsignal_srs_cfg_t srs_cfg;
  srslte_pucch_sched_t pucch_sched;  
} srslte_enb_ul_user_t;
```

### srslte\_enb\_ul\_t

Location: `./lib/include/srslte/phy/enb/enb_ul.h`

```c++
typedef struct SRSLTE_API {
  srslte_cell_t cell;

  cf_t *sf_symbols; 
  cf_t *ce; 

  srslte_ofdm_t     fft;
  srslte_chest_ul_t chest;

  srslte_pusch_t  pusch;
  srslte_pucch_t  pucch;
  srslte_prach_t  prach;

  srslte_pusch_cfg_t     pusch_cfg; 

  srslte_pusch_hopping_cfg_t hopping_cfg;

  // Configuration for each user
  srslte_enb_ul_user_t **users; 

} srslte_enb_ul_t;
```

### srslte\_enb\_ul\_pusch\_t

Location: `./lib/include/srslte/phy/enb/enb_ul.h`

```c++
typedef struct {
  uint16_t                rnti; 
  srslte_ra_ul_dci_t      grant;
  srslte_dci_location_t   location; 
  uint32_t                rv_idx; 
  uint32_t                current_tx_nb; 
  uint8_t                *data; 
  srslte_softbuffer_rx_t *softbuffer;
  bool                    needs_pdcch; 
} srslte_enb_ul_pusch_t;
```

## fec

Forward error correction.

### srslte\_cbsegm\_t

Location: `./lib/include/srslte/phy/fec/cbsegm.h`

```c++
 typedef struct SRSLTE_API {
  uint32_t F;
  uint32_t C;
  uint32_t K1;
  uint32_t K2;
  uint32_t K1_idx;
  uint32_t K2_idx;
  uint32_t C1;
  uint32_t C2;
  uint32_t tbs; 
} srslte_cbsegm_t;
```

### srslte\_convcoder\_t

Location: `./lib/include/srslte/phy/fec/convcoder.h`

```c++
typedef struct SRSLTE_API {
  uint32_t R;
  uint32_t K;
  int poly[3];
  bool tail_biting;
}srslte_convcoder_t;
```

### srslte\_crc\_t

Location: `./lib/include/srslte/phy/fec/crc.h`

```c++
typedef struct SRSLTE_API {
  uint64_t table[256];
  int polynom;
  int order;
  uint64_t crcinit; 
  uint64_t crcmask;
  uint64_t crchighbit;
  uint32_t srslte_crc_out;
} srslte_crc_t;
```

### srslte\_softbuffer\_rx\_t

Location: `./lib/include/srslte/phy/fec/softbuffer.h`

```c++
typedef struct SRSLTE_API {
  uint32_t max_cb;
  int16_t **buffer_f;
} srslte_softbuffer_rx_t;
```

### srslte\_softbuffer\_tx\_t

Location: `./lib/include/srslte/phy/fec/softbuffer.h`

```c++
typedef struct SRSLTE_API {
  uint32_t max_cb;
  uint8_t **buffer_b;
} srslte_softbuffer_tx_t;
```

### srslte\_tc\_interl\_t

Location: `./lib/include/srslte/phy/fec/tc_interl.h`

```c++
typedef struct SRSLTE_API {
  uint16_t *forward;
  uint16_t *reverse;
  uint32_t max_long_cb;
} srslte_tc_interl_t;
```

### srslte\_tcod\_t

Location: `./lib/include/srslte/phy/fec/turbocoder.h`

```c++
typedef struct SRSLTE_API {
  uint32_t max_long_cb;
  uint8_t *temp;
} srslte_tcod_t;
```

### srslte\_tdec\_t

Location: `./lib/include/srslte/phy/fec/turbodecoder.h`

```c++
typedef struct SRSLTE_API {
  float *input_conv;
  union {
    srslte_tdec_simd_t tdec_simd;
    srslte_tdec_gen_t  tdec_gen;
  };
} srslte_tdec_t;
```

### srslte\_map\_gen\_vl\_t

Location: `./lib/include/srslte/phy/fec/turbodecoder_gen.h`

```c++
typedef struct SRSLTE_API {
  int max_long_cb;
  float *beta;
} srslte_map_gen_vl_t;
```

### srslte\_tdec\_gen\_t

Location: `./lib/include/srslte/phy/fec/turbodecoder_gen.h`

```c++
typedef struct SRSLTE_API {
  int max_long_cb;

  srslte_map_gen_vl_t dec;

  float *llr1;
  float *llr2;
  float *w;
  float *syst;
  float *parity;

  int current_cbidx; 
  uint32_t current_cb_len;
  uint32_t n_iter; 
  srslte_tc_interl_t interleaver[SRSLTE_NOF_TC_CB_SIZES];
} srslte_tdec_gen_t;
```

### map\_gen\_t

Location: `./lib/include/srslte/phy/fec/turbodecoder_simd.h`

```c++
typedef struct SRSLTE_API {
  uint32_t max_long_cb;
  uint32_t max_par_cb; 
  int16_t *alpha;
  int16_t *branch;
} map_gen_t;
```

### srslte\_tdec\_simd\_t

Location: `./lib/include/srslte/phy/fec/turbodecoder_simd.h`

```c++
typedef struct SRSLTE_API {
  uint32_t max_long_cb;
  uint32_t max_par_cb; 

  map_gen_t dec;

  int16_t *app1[SRSLTE_TDEC_MAX_NPAR];
  int16_t *app2[SRSLTE_TDEC_MAX_NPAR];
  int16_t *ext1[SRSLTE_TDEC_MAX_NPAR];
  int16_t *ext2[SRSLTE_TDEC_MAX_NPAR];
  int16_t *syst[SRSLTE_TDEC_MAX_NPAR];
  int16_t *parity0[SRSLTE_TDEC_MAX_NPAR];
  int16_t *parity1[SRSLTE_TDEC_MAX_NPAR];

  int cb_mask; 
  int current_cbidx; 
  srslte_tc_interl_t interleaver[SRSLTE_NOF_TC_CB_SIZES];
  int n_iter[SRSLTE_TDEC_MAX_NPAR];
} srslte_tdec_simd_t;
```

### srslte\_tdec\_simd\_inter\_t

Location: `./lib/include/srslte/phy/fec/turbodecoder_simd_inter.h`

```c++
typedef struct SRSLTE_API {
  int max_long_cb;

  int16_t *syst0;
  int16_t *parity0;
  int16_t *syst1;
  int16_t *parity1;
  int16_t *llr1;
  int16_t *llr2;
  int16_t *w;
  int16_t *alpha;

  uint32_t max_par_cb;   
  int current_cbidx; 
  uint32_t current_long_cb;
  srslte_tc_interl_t interleaver[SRSLTE_NOF_TC_CB_SIZES];
  int n_iter[SRSLTE_TDEC_MAX_NPAR];
} srslte_tdec_simd_inter_t;
```

### map\_gen\_t

Location: `./lib/include/srslte/phy/fec/turbodecoder_sse.h`

```c++
typedef struct SRSLTE_API {
  int max_long_cb;
  int16_t *alpha;
  int16_t *branch;
} map_gen_t;
```

### srslte\_tdec\_sse\_t

Location: `./lib/include/srslte/phy/fec/turbodecoder_sse.h`

```c++
typedef struct SRSLTE_API {
  int max_long_cb;

  map_gen_t dec;

  int16_t *app1;
  int16_t *app2;
  int16_t *ext1;
  int16_t *ext2;
  int16_t *syst;
  int16_t *parity0;
  int16_t *parity1;

  int current_cbidx; 
  srslte_tc_interl_t interleaver[SRSLTE_NOF_TC_CB_SIZES];
  int n_iter;
} srslte_tdec_sse_t;
```

### srslte\_viterbi\_type\_t

Location: `./lib/include/srslte/phy/fec/viterbi.h`

```c++
typedef enum {
  SRSLTE_VITERBI_27 = 0, 
  SRSLTE_VITERBI_29, 
  SRSLTE_VITERBI_37, 
  SRSLTE_VITERBI_39
}srslte_viterbi_type_t;
```

### srslte\_viterbi\_t

Location: `./lib/include/srslte/phy/fec/viterbi.h`

```c++
typedef struct SRSLTE_API{
  void *ptr;
  uint32_t R;
  uint32_t K;
  uint32_t framebits;
  bool tail_biting;
  float gain_quant; 
  int16_t gain_quant_s; 
  int (*decode) (void*, uint8_t*, uint8_t*, uint32_t);
  int (*decode_s) (void*, uint16_t*, uint8_t*, uint32_t);
  int (*decode_f) (void*, float*, uint8_t*, uint32_t);
  void (*free) (void*);
  uint8_t *tmp;
  uint16_t *tmp_s;
  uint8_t *symbols_uc;
  uint16_t *symbols_us;
}srslte_viterbi_t;
```

## io

I/O. File sink, file source, net sink, net source.

### srslte\_binsource\_t

Location: `./lib/include/srslte/phy/io/binsource.h`

```c++
typedef struct SRSLTE_API{
  uint32_t seed;
  uint32_t *seq_buff;
  int seq_buff_nwords;
  int seq_cache_nbits;
  int seq_cache_rp;
}srslte_binsource_t;
```

Low-level API.

### srslte\_filesink\_t

Location: `./lib/include/srslte/phy/io/filesink.h`

```c++
typedef struct SRSLTE_API {
  FILE *f;
  srslte_datatype_t type;
} srslte_filesink_t;
```

### srslte\_filesource\_t

Location: `./lib/include/srslte/phy/io/filesource.h`

```c++
typedef struct SRSLTE_API {
  FILE *f;
  srslte_datatype_t type;
} srslte_filesource_t;
```

### srslte\_datatype\_t

Location: `./lib/include/srslte/phy/io/format.h`

```c++
typedef enum { 
  SRSLTE_FLOAT, 
  SRSLTE_COMPLEX_FLOAT, 
  SRSLTE_COMPLEX_SHORT, 
  SRSLTE_FLOAT_BIN, 
  SRSLTE_COMPLEX_FLOAT_BIN, 
  SRSLTE_COMPLEX_SHORT_BIN  
} srslte_datatype_t;
```

Data types used in srsLTE library.

### srslte\_netsink\_type\_t

Location: `./lib/include/srslte/phy/io/netsink.h`

```c++
typedef enum {
  SRSLTE_NETSINK_UDP, 
  SRSLTE_NETSINK_TCP  
} srslte_netsink_type_t; 
```

### srslte\_netsink\_t

Location: `./lib/include/srslte/phy/io/netsink.h`

```c++
typedef struct SRSLTE_API {
  int sockfd;
  bool connected;
  srslte_netsink_type_t type; 
  struct sockaddr_in servaddr;
}srslte_netsink_t;
```

### srslte\_netsource\_type\_t

Location: `./lib/include/srslte/phy/io/netsource.h`

```c++
typedef enum {
  SRSLTE_NETSOURCE_UDP, 
  SRSLTE_NETSOURCE_TCP  
} srslte_netsource_type_t; 
```

### srslte\_netsource\_t

Location: `./lib/include/srslte/phy/io/netsource.h`

```c++
typedef struct SRSLTE_API {
  int sockfd;
  int connfd; 
  struct sockaddr_in servaddr;
  srslte_netsource_type_t type; 
  struct sockaddr_in cliaddr;  
}srslte_netsource_t;
```

## modem

### srslte\_demod\_hard\_t

Location: `./lib/include/srslte/phy/modem/demod_hard.h`

```c++
typedef struct SRSLTE_API {
  srslte_mod_t mod; /* In this implementation, mapping table is hard-coded */
}srslte_demod_hard_t;
```

### bpsk\_packed\_t

Location: `./lib/include/srslte/phy/modem/modem_table.h`

```c++
typedef struct {
  cf_t symbol[8];
} bpsk_packed_t;
```

### qpsk\_packed\_t

Location: `./lib/include/srslte/phy/modem/modem_table.h`

```c++
typedef struct {
  cf_t symbol[4];
} qpsk_packed_t;
```

### qam16\_packed\_t

Location: `./lib/include/srslte/phy/modem/modem_table.h`

```c++
typedef struct {
  cf_t symbol[2];
} qam16_packed_t;
```

### srslte\_modem\_table\_t

Location: `./lib/include/srslte/phy/modem/modem_table.h`

```c++
typedef struct SRSLTE_API {
  cf_t* symbol_table;             // bit-to-symbol mapping
  uint32_t nsymbols;              // number of modulation symbols
  uint32_t nbits_x_symbol;        // number of bits per symbol

  bool byte_tables_init;
  bpsk_packed_t *symbol_table_bpsk;
  qpsk_packed_t *symbol_table_qpsk;
  qam16_packed_t *symbol_table_16qam;  
}srslte_modem_table_t;
```

## resampling

### srslte\_resample\_arb\_t

Location: `./lib/include/srslte/phy/resampling/resample_arb.h`

```c++
typedef struct SRSLTE_API {
  float rate;                // Resample rate
  float step;                // Step increment through filter
  float acc;                 // Index into filter
  bool interpolate;
  cf_t reg[SRSLTE_RESAMPLE_ARB_M];  // Our window of samples

} srslte_resample_arb_t;
```

## rf

### srslte\_rf\_t

Location: `./lib/include/srslte/phy/rf/rf.h`

```c++
typedef struct {
  void *handler;
  void *dev;

  // The following variables are for threaded RX gain control 
  pthread_t thread_gain; 
  pthread_cond_t  cond; 
  pthread_mutex_t mutex; 
  double cur_rx_gain; 
  double new_rx_gain;   
  bool   tx_gain_same_rx; 
  float  tx_rx_gain_offset; 
} srslte_rf_t;
```

### srslte\_rf\_cal\_t

Location: `./lib/include/srslte/phy/rf/rf.h`

```c++
typedef struct {
  float dc_gain;
  float dc_phase;
  float iq_i;
  float iq_q; 
} srslte_rf_cal_t;
```

### srslte\_rf\_error\_t

Location: `./lib/include/srslte/phy/rf/rf.h`

```c++
typedef struct {
  enum { 
    SRSLTE_RF_ERROR_LATE,
    SRSLTE_RF_ERROR_UNDERFLOW,
    SRSLTE_RF_ERROR_OVERFLOW,
    SRSLTE_RF_ERROR_OTHER
  } type;
  int opt;
  const char *msg; 
} srslte_rf_error_t;
```

### cell\_search\_cfg\_t

Location: `./lib/include/srslte/phy/rf/rf_utils.h`

```c++
typedef struct SRSLTE_API {
  uint32_t max_frames_pbch;      // timeout in number of 5ms frames for MIB decoding
  uint32_t max_frames_pss;       // timeout in number of 5ms frames for synchronization
  uint32_t nof_valid_pss_frames; // number of required synchronized frames
  float init_agc; // 0 or negative to disable AGC  
} cell_search_cfg_t;
```

## sync

### srslte\_cfo\_t

Location: `./lib/include/srslte/phy/sync/cfo.h`

```c++
typedef struct SRSLTE_API {
  float last_freq;
  float tol;
  int nsamples;
  int max_samples;
  srslte_cexptab_t tab;
  cf_t *cur_cexp;
}srslte_cfo_t;
```

### srslte\_cp\_synch\_t

Location: `./lib/include/srslte/phy/sync/cp.h`

```c++
typedef struct {
  cf_t *corr;
  uint32_t symbol_sz;
  uint32_t max_symbol_sz;
} srslte_cp_synch_t;
```

### srslte\_pss\_t

Location: `./lib/include/srslte/phy/sync/pss.h`

```c++
typedef struct SRSLTE_API {

#ifdef CONVOLUTION_FFT
  srslte_conv_fft_cc_t conv_fft;
  srslte_filt_cc_t filter;

#endif
  int decimate;

  uint32_t max_frame_size;
  uint32_t max_fft_size;

  uint32_t frame_size;
  uint32_t N_id_2;
  uint32_t fft_size;
  cf_t *pss_signal_freq_full[3];

  cf_t *pss_signal_time[3];
  cf_t *pss_signal_time_scale[3];

  cf_t pss_signal_freq[3][SRSLTE_PSS_LEN]; // One sequence for each N_id_2
  cf_t *tmp_input;
  cf_t *conv_output;
  float *conv_output_abs;
  float ema_alpha;
  float *conv_output_avg;
  float peak_value;

  bool filter_pss_enable;
  srslte_dft_plan_t dftp_input;
  srslte_dft_plan_t idftp_input;
  cf_t tmp_fft[SRSLTE_SYMBOL_SZ_MAX];
  cf_t tmp_fft2[SRSLTE_SYMBOL_SZ_MAX];

  cf_t tmp_ce[SRSLTE_PSS_LEN];

  bool chest_on_filter;

}srslte_pss_t;
```

### pss\_direction\_t

Location: `./lib/include/srslte/phy/sync/pss.h`

```c++
typedef enum { PSS_TX, PSS_RX } pss_direction_t;
```

### srslte\_sss\_tables\_t

Location: `./lib/include/srslte/phy/sync/sss.h`

```c++
typedef struct SRSLTE_API {
  int z1[SRSLTE_SSS_N][SRSLTE_SSS_N];
  int c[2][SRSLTE_SSS_N];
  int s[SRSLTE_SSS_N][SRSLTE_SSS_N];
}srslte_sss_tables_t;
```

### srslte\_sss\_fc\_tables\_t

Location: `./lib/include/srslte/phy/sync/sss.h`

```c++
typedef struct SRSLTE_API {
  float z1[SRSLTE_SSS_N][SRSLTE_SSS_N];
  float c[2][SRSLTE_SSS_N];
  float s[SRSLTE_SSS_N][SRSLTE_SSS_N];
  float sd[SRSLTE_SSS_N][SRSLTE_SSS_N-1];
}srslte_sss_fc_tables_t;
```

Allocate 32 complex to make it multiple of 32-byte AVX instructions alignment requirement. Should use srslte\_vec\_malloc() to make it platform agnostic.

### srslte\_sss\_t

Location: `./lib/include/srslte/phy/sync/sss.h`

```c++
typedef struct SRSLTE_API {

  srslte_dft_plan_t dftp_input;

  uint32_t fft_size;
  uint32_t max_fft_size;

  float corr_peak_threshold;
  uint32_t symbol_sz;
  uint32_t subframe_sz;
  uint32_t N_id_2;

  uint32_t N_id_1_table[30][30];
  srslte_sss_fc_tables_t fc_tables[3]; // one for each N_id_2

  float corr_output_m0[SRSLTE_SSS_N];
  float corr_output_m1[SRSLTE_SSS_N];

}srslte_sss_t;
```

### sss\_alg\_t

Location: `./lib/include/srslte/phy/sync/sync.h`

```c++
typedef enum {SSS_DIFF=0, SSS_PARTIAL_3=2, SSS_FULL=1} sss_alg_t;
```

### srslte\_sync\_t

Location: `./lib/include/srslte/phy/sync/sync.h`

```c++
typedef struct SRSLTE_API {
  srslte_pss_t pss;
  srslte_pss_t pss_i[2];
  srslte_sss_t sss;
  srslte_cp_synch_t cp_synch;
  cf_t *cfo_i_corr[2];
  int decimate;
  float threshold;
  float peak_value;
  uint32_t N_id_2;
  uint32_t N_id_1;
  uint32_t sf_idx;
  uint32_t fft_size;
  uint32_t frame_size;
  uint32_t max_offset;
  uint32_t nof_symbols;
  uint32_t cp_len;
  float current_cfo_tol;
  sss_alg_t sss_alg; 
  bool detect_cp;
  bool sss_en;
  srslte_cp_t cp;
  uint32_t m0;
  uint32_t m1;
  float m0_value;
  float m1_value;
  float M_norm_avg; 
  float M_ext_avg; 
  cf_t  *temp;

  uint32_t max_frame_size;


  // variables for various CFO estimation methods
  bool cfo_cp_enable;
  bool cfo_pss_enable;
  bool cfo_i_enable;

  bool cfo_cp_is_set;
  bool cfo_pss_is_set;
  bool cfo_i_initiated;

  float cfo_cp_mean;
  float cfo_pss;
  float cfo_pss_mean;
  int   cfo_i_value;

  float cfo_ema_alpha;

  uint32_t cfo_cp_nsymbols;

  srslte_cfo_t cfo_corr_frame;
  srslte_cfo_t cfo_corr_symbol;

  bool sss_channel_equalize;
  bool pss_filtering_enabled;
  cf_t sss_filt[SRSLTE_SYMBOL_SZ_MAX];
  cf_t pss_filt[SRSLTE_SYMBOL_SZ_MAX];

}srslte_sync_t;
```

### srslte\_sync\_find\_ret\_t

Location: `./lib/include/srslte/phy/sync/sync.h`

```c++
typedef enum {
  SRSLTE_SYNC_FOUND = 1, 
  SRSLTE_SYNC_FOUND_NOSPACE = 2, 
  SRSLTE_SYNC_NOFOUND = 0, 
  SRSLTE_SYNC_ERROR = -1  
} srslte_sync_find_ret_t;
```

## ue

### srslte\_ue\_cellsearch\_result\_t

Location: `./lib/include/srslte/phy/ue/ue_cell_search.h`

```c++
typedef struct SRSLTE_API {
  uint32_t cell_id;
  srslte_cp_t cp; 
  float peak; 
  float mode; 
  float psr;
  float cfo; 
} srslte_ue_cellsearch_result_t;
```

### srslte\_ue\_cellsearch\_t

Location: `./lib/include/srslte/phy/ue/ue_cell_search.h`

```c++
typedef struct SRSLTE_API {
  srslte_ue_sync_t ue_sync;

  cf_t *sf_buffer[SRSLTE_MAX_PORTS];
  uint32_t nof_rx_antennas; 

  uint32_t max_frames;
  uint32_t nof_valid_frames;  // number of 5 ms frames to scan 

  uint32_t *mode_ntimes;
  uint8_t *mode_counted; 

  srslte_ue_cellsearch_result_t *candidates; 
} srslte_ue_cellsearch_t;
```

### dci\_blind\_search\_t

Location: `./lib/include/srslte/phy/ue/ue_dl.h`

```c++
typedef struct {
  srslte_dci_format_t format; 
  srslte_dci_location_t loc[MAX_CANDIDATES];
  uint32_t nof_locations; 
} dci_blind_search_t;
```

### srslte\_ue\_dl\_t

Location: `./lib/include/srslte/phy/ue/ue_dl.h`

```c++
typedef struct SRSLTE_API {
  srslte_pcfich_t pcfich;
  srslte_pdcch_t pdcch;
  srslte_pdsch_t pdsch;
  srslte_pmch_t  pmch;
  srslte_phich_t phich; 
  srslte_regs_t regs;
  srslte_ofdm_t fft[SRSLTE_MAX_PORTS];
  srslte_ofdm_t fft_mbsfn;
  srslte_chest_dl_t chest;

  srslte_cfo_t sfo_correct; 

  srslte_pdsch_cfg_t pdsch_cfg;
  srslte_pdsch_cfg_t pmch_cfg;
  srslte_softbuffer_rx_t *softbuffers[SRSLTE_MAX_CODEWORDS];
  srslte_ra_dl_dci_t dl_dci;
  srslte_cell_t cell;

  uint32_t nof_rx_antennas;

  cf_t *sf_symbols;  // this is for backwards compatibility
  cf_t *sf_symbols_m[SRSLTE_MAX_PORTS]; 
  cf_t *ce[SRSLTE_MAX_PORTS]; // compatibility
  cf_t *ce_m[SRSLTE_MAX_PORTS][SRSLTE_MAX_PORTS];

  /* RI, PMI and SINR for MIMO statistics */
  float sinr[SRSLTE_MAX_LAYERS][SRSLTE_MAX_CODEBOOKS];
  uint32_t pmi[SRSLTE_MAX_LAYERS];
  uint32_t ri;

  /* Power allocation parameter 3GPP 36.213 Clause 5.2 Rho_b */
  float rho_b;

  srslte_dci_format_t dci_format;
  uint64_t pkt_errors; 
  uint64_t pkts_total;
  uint64_t pdsch_pkt_errors;
  uint64_t pdsch_pkts_total;
  uint64_t pmch_pkt_errors;
  uint64_t pmch_pkts_total;
  uint64_t nof_detected; 

  uint16_t current_rnti;
  uint16_t current_mbsfn_area_id;
  dci_blind_search_t current_ss_ue[3][10];
  dci_blind_search_t current_ss_common[3];
  srslte_dci_location_t last_location;
  srslte_dci_location_t last_location_ul;

  srslte_dci_msg_t pending_ul_dci_msg; 
  uint16_t pending_ul_dci_rnti; 

  float sample_offset;

  float last_phich_corr;
}srslte_ue_dl_t;
```

### srslte\_ue\_mib\_t

Location: `./lib/include/srslte/phy/ue/ue_mib.h`

```c++
typedef struct SRSLTE_API {
  srslte_sync_t sfind;

  cf_t *sf_symbols;
  cf_t *ce[SRSLTE_MAX_PORTS];

  srslte_ofdm_t fft;
  srslte_chest_dl_t chest; 
  srslte_pbch_t pbch;

  uint8_t bch_payload[SRSLTE_BCH_PAYLOAD_LEN];
  uint32_t nof_tx_ports; 
  uint32_t sfn_offset; 

  uint32_t frame_cnt; 
} srslte_ue_mib_t;
```

### srslte\_ue\_sync\_state\_t

Location: `./lib/include/srslte/phy/ue/ue_sync.h`

```c++
typedef enum SRSLTE_API { SF_FIND, SF_TRACK} srslte_ue_sync_state_t;
```

### srslte\_ue\_sync\_t

Location: `./lib/include/srslte/phy/ue/ue_sync.h`

```c++
typedef struct SRSLTE_API {
  srslte_sync_t sfind;
  srslte_sync_t strack;

  uint32_t max_prb;

  srslte_agc_t agc; 
  bool do_agc; 
  uint32_t agc_period; 
  int decimate;
  void *stream; 
  void *stream_single; 
  int (*recv_callback)(void*, cf_t*[SRSLTE_MAX_PORTS], uint32_t, srslte_timestamp_t*);
  int (*recv_callback_single)(void*, void*, uint32_t, srslte_timestamp_t*); 
  srslte_timestamp_t last_timestamp;

  uint32_t nof_rx_antennas; 

  srslte_filesource_t file_source; 
  bool file_mode; 
  float file_cfo;
  bool file_wrap_enable;
  srslte_cfo_t file_cfo_correct; 

  srslte_ue_sync_state_t state;

  uint32_t frame_len; 
  uint32_t fft_size;
  uint32_t nof_recv_sf;  // Number of subframes received each call to srslte_ue_sync_get_buffer
  uint32_t nof_avg_find_frames;
  uint32_t frame_find_cnt;
  uint32_t sf_len;

  /* These count half frames (5ms) */
  uint64_t frame_ok_cnt;
  uint32_t frame_no_cnt; 
  uint32_t frame_total_cnt; 

  /* this is the system frame number (SFN) */
  uint32_t frame_number; 

  srslte_cell_t cell; 
  uint32_t sf_idx;

  bool decode_sss_on_track; 

  bool  cfo_is_copied;
  bool  cfo_correct_enable_track;
  bool  cfo_correct_enable_find;
  float cfo_current_value;
  float cfo_loop_bw_pss;
  float cfo_loop_bw_ref;
  float cfo_pss_min;
  float cfo_ref_min;
  float cfo_ref_max;

  uint32_t pss_stable_cnt;
  uint32_t pss_stable_timeout;
  bool     pss_is_stable;

  uint32_t peak_idx;
  int next_rf_sample_offset;
  int last_sample_offset; 
  float mean_sample_offset; 
  float mean_sfo; 
  uint32_t sample_offset_correct_period; 
  float sfo_ema; 


  #ifdef MEASURE_EXEC_TIME
  float mean_exec_time;
  #endif
} srslte_ue_sync_t;
```

### srslte\_ue\_ul\_powerctrl\_t

Location: `./lib/include/srslte/phy/ue/ue_ul.h`

```c++
typedef struct {
  // Common configuration
  float p0_nominal_pusch;
  float alpha;
  float p0_nominal_pucch;
  float delta_f_pucch[5];
  float delta_preamble_msg3;

  // Dedicated configuration
  float p0_ue_pusch;
  bool delta_mcs_based;
  bool acc_enabled;
  float p0_ue_pucch;
  float p_srs_offset;  
} srslte_ue_ul_powerctrl_t;
```

UE UL power control.

### srslte\_ue\_ul\_t

Location: `./lib/include/srslte/phy/ue/ue_ul.h`

```c++
typedef struct SRSLTE_API {
  srslte_ofdm_t fft;
  srslte_cfo_t cfo; 
  srslte_cell_t cell;

  bool normalize_en; 
  bool cfo_en; 

  float current_cfo_tol;
  float current_cfo; 
  srslte_pucch_format_t last_pucch_format;

  srslte_pusch_cfg_t pusch_cfg; 
  srslte_refsignal_ul_t signals; 
  srslte_refsignal_ul_dmrs_pregen_t pregen_drms;
  srslte_refsignal_srs_pregen_t pregen_srs;

  srslte_softbuffer_tx_t softbuffer;

  srslte_pusch_t pusch; 
  srslte_pucch_t pucch; 

  srslte_pucch_sched_t              pucch_sched; 
  srslte_refsignal_srs_cfg_t        srs_cfg;
  srslte_uci_cfg_t                  uci_cfg;
  srslte_pusch_hopping_cfg_t        hopping_cfg;
  srslte_ue_ul_powerctrl_t          power_ctrl;

  cf_t *refsignal; 
  cf_t *srs_signal; 
  cf_t *sf_symbols; 

  uint16_t current_rnti;  
  bool signals_pregenerated;
}srslte_ue_ul_t;
```

## utils

### srslte\_bit\_interleaver\_t

Location: `./lib/include/srslte/phy/utils/bit.h`

```c++
typedef struct {
  uint32_t nof_bits;
  uint16_t *interleaver;
  uint16_t *byte_idx;
  uint8_t *bit_mask;
  uint8_t n_128;
} srslte_bit_interleaver_t;
```

### srslte\_cexptab\_t

Location: `./lib/include/srslte/phy/utils/cexptab.h`

```c++
typedef struct SRSLTE_API {
  uint32_t size;
  cf_t *tab;
}srslte_cexptab_t;
```

### srslte\_conv\_fft\_cc\_t

Location: `./lib/include/srslte/phy/utils/convolution.h`

```c++
typedef struct SRSLTE_API {
  cf_t *input_fft;
  cf_t *filter_fft;
  cf_t *output_fft;
  cf_t *output_fft2;
  uint32_t input_len;
  uint32_t filter_len;
  uint32_t output_len;
  uint32_t max_input_len;
  uint32_t max_filter_len;
  srslte_dft_plan_t input_plan;
  srslte_dft_plan_t filter_plan;
  srslte_dft_plan_t output_plan;
  //cf_t *pss_signal_time_fft[3]; // One sequence for each N_id_2
  //cf_t *pss_signal_time[3];

}srslte_conv_fft_cc_t;
```

### srslte\_filt\_cc\_t

Location: `./lib/include/srslte/phy/utils/filter.h`

```c++
typedef struct SRSLTE_API{
    cf_t *filter_input;
    cf_t *downsampled_input;
    cf_t *filter_output;
    bool is_decimator;
    int factor;
    int num_taps;
    float *taps;

}srslte_filt_cc_t;
```

### srslte\_ringbuffer\_t

Location: `./lib/include/srslte/phy/utils/ringbuffer.h`

```c++
typedef struct {
  uint8_t *buffer;
  bool active;
  int capacity; 
  int count; 
  int wpm; 
  int rpm; 
  pthread_mutex_t mutex; 
  pthread_cond_t  cvar; 
} srslte_ringbuffer_t; 
```
