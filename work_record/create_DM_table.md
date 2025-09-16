CREATE TABLE IF NOT EXISTS BIDWADM_CO.DM_FI_SLP_CASH
(
  -- Business key
  ACUNIT_CD            VARCHAR(20)   NOT NULL,
  SLP_NO               VARCHAR(50)   NOT NULL,
  SLP_LNO              INTEGER       NOT NULL,

  -- Attributes & measures
  SLP_TP_CD            VARCHAR(10),
  SLP_JOUR_TP_CD       VARCHAR(10),
  ACNT_CD              VARCHAR(50),

  CRNCY_CD             VARCHAR(10),
  DR_AMT               NUMERIC(18,2),
  CR_AMT               NUMERIC(18,2),

  COMP_CRNCY_CD        VARCHAR(10),
  COMP_CRNCY_DR_AMT    NUMERIC(18,2),
  COMP_CRNCY_CR_AMT    NUMERIC(18,2),

  APRV_DT              TIMESTAMP,
  REG_DTTM             TIMESTAMP,
  MOD_DTTM             TIMESTAMP,
  SLP_DT               DATE          NOT NULL,  

  -- Org / Company
  ACUNIT_NM            VARCHAR(200),
  ACUNIT_ABBR_NM       VARCHAR(50),
  COMP_CD              VARCHAR(20),
  COMP_NM              VARCHAR(200),
  COMP_ABBR_NM         VARCHAR(50),

  -- Account master
  ACNT_NM              VARCHAR(200),
  ACNT_ENG_NM          VARCHAR(200),

  -- Audit
  ETL_LOAD_DTTM        TIMESTAMP     DEFAULT CURRENT_TIMESTAMP
)
PARTITION BY date_trunc('month', SLP_DT)
;
