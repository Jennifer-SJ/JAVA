1. 建主表（模板表）
`CREATE TABLE IF NOT EXISTS db_label_task (
    id               VARCHAR(64) NOT NULL,
    name             VARCHAR(64) NOT NULL,
    project_id       VARCHAR(64) NOT NULL,
    batch_task_id    VARCHAR(64) NOT NULL,
    status           VARCHAR(64) NOT NULL,
    sample_statistic BIGINT[]    DEFAULT '{0,0}'::BIGINT[],
    frame_id_idx     BIGINT      DEFAULT '-1'::INTEGER,
    start_at         BIGINT      NOT NULL,
    update_at        BIGINT      DEFAULT '0'::INTEGER,
    partition_id     INTEGER
) PARTITION BY RANGE (partition_id);`

2. 建第一个分区（子表）
`CREATE TABLE IF NOT EXISTS db_label_task_20240101
    PARTITION OF db_label_task
    FOR VALUES FROM (20230701) TO (20240101);`
