# 巡展平板离线配发资料

以下台账为合成数据，不涉及真实访客、供应商或展馆。CSV 采用 UTF-8，首行为字段名，空字段代表源资料未给出。标识仅在字段明示的实体范围内使用。`data/agreements.json` 是当期业务方提供的运营资料，`data/formats.json` 记录文件列顺序和确定的外键引用。

- `data/pages.csv` 记录内容页面正常顺序、相关的体验模式及是否可跳过。列为 `page`、`order`、`required_mode`、`optional`。
- `data/assets.csv` 记录完整件与差量的版本、大小及适用设备。approved_from 为内容登记日。列为 `asset`、`component`、`version`、`kib`、`approved_from`、`device_type`、`package`。
- `data/dependencies.csv` 记录给定版本的页面所需资源，optional_group 非零时该编号的同类可替代，零为必需。列为 `page`、`version`、`mode`、`asset`、`optional_group`。
- `data/cohorts.csv` 记录团级需求及决策收到资料的日截止。列为 `cohort`、`day`、`venue`、`route`、`start`、`size`、`mode`、`cutoff`、`partition`。
- `data/requests.csv` 记录领取后请求，未构成访问与已观察但打开失败的原因分开。列为 `request`、`cohort`、`device`、`page`、`version`、`minute`、`trigger`、`request_frame`。
- `data/results.csv` 记录打开确认、缺素材或备用引导回执。列为 `request`、`minute`、`state`、`fallback_step`、`known_day`。
- `data/installed.csv` 记录历史安装结果和装配方式；传输包大小见资产目录。列为 `cohort`、`device`、`device_type`、`asset`、`day`、`minute`、`state`、`delivery`。
- `data/future_tours.csv` 记录下一期团要求，first/last 是界定团讲范围的展段顺序。列为 `cohort`、`mode`、`first`、`last`、`allow_backup`、`announced`。
- `data/issued.csv` 记录未来团已经触达的设备和确认的资产。列为 `receipt`、`cohort`、`device`、`device_type`、`asset`、`minute`、`state`、`space_kib`。
- `data/slots.csv` 记录团体入场前仍能选择的共享连接资源。列为 `window`、`start`、`end`、`kib`、`venue`。
- `data/options.csv` 记录可用下载选项及已知要保留的辅助/语言承诺。required_from 是应用该差量的原版。列为 `proposal`、`cohort`、`device`、`window`、`asset`、`required_from`、`guarantees`。
- `data/revision.csv` 记录内容方给出的勘误及可用替代。列为 `memo`、`asset`、`minute`、`action`、`substitute`。
- `data/transfer_receipts.csv` 记录明确区分抵达、安装和届时仍不确定的回报。列为 `event`、`proposal`、`minute`、`state`、`transferred_kib`。
- `data/fallbacks.csv` 记录馆员给各设备领取人备纸质说明的确认时点和适用的展页、体验模式。勘误的 `substitute` 引用备用说明编号。

使用 Python 3.11，无第三方依赖。用 `python3 -m unittest discover -s tests -v` 核对文件的可读性、列结构和确定引用，源文件保持只读。
