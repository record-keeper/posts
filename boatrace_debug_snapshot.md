# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-26T14:00:02.165871+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×41 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×11 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-26T14:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×35  [2026-07-26T13:24:52]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×82  [2026-07-26T13:19:27]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×114  [2026-07-26T13:02:26]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×57  [2026-07-26T13:02:26]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-26T13:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×20  [2026-07-26T10:31:20]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ORPHAN_SCAN  ×1  [2026-07-26T06:00:08]
- key: `ORPHAN_SCAN|175 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-26T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=77<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-26T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S00: n=182<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-26T06:00:08]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=80 hit%=33.8% ROI=0.82 (コスト 18,300/回収 14,930)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-26T06:00:08]
- key: `DRIFT_BUCKET|drift ≥+30%: n=38 hit%=23.7% ROI=0.67 (コスト 10,500/回収 6,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-26T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=13 pred=0.2273 actual=0.3077 gap=-0.0804`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-26T06:00:08]
- key: `ROI_STAT|S00: n=182 hit%=28.6% hit_CI[Bonf]=[20.0,39.0]% ROI=0.77 ROI_boot95=[0.57,0.98]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-26T06:00:08]
- key: `ROI_STAT|S01_NAKAANA1: n=165 hit%=26.7% hit_CI[Bonf]=[18.0,37.5]% ROI=0.75 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-26T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=165<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-26T06:00:08]
- key: `ROI_STAT|S02_TETSUBAN: n=77 hit%=50.6% hit_CI[Bonf]=[35.0,66.2]% ROI=1.00 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-26T06:00:08]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=28.6% ROI=0.59 (コスト 10,300/回収 6,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-26T06:00:08]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=42 hit%=31.0% ROI=0.89 (コスト 10,200/回収 9,070)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-26T06:00:08]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=35 hit%=25.7% ROI=0.52 (コスト 8,200/回収 4,290)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 8.77MB / last modified 2026-07-26T14:00:04.861605+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
0), retry in 9s
2026-07-26 13:58:38,259 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=21&hd=20260726
2026-07-26 13:58:38,259 [ERROR] scraper: racelist fetch failed: jcd=21 rno=12
2026-07-26 13:58:38,259 [WARNING] run_cycle: fetch None: 21/12
2026-07-26 13:58:49,695 [INFO] scraper: odds3t: 120/120 parsed
2026-07-26 13:58:50,780 [INFO] scraper: odds3f: 20/20 parsed
2026-07-26 13:58:51,883 [INFO] scraper: odds2t: 29/30 parsed
2026-07-26 13:58:51,885 [INFO] scraper: odds2f: 14/15 parsed
2026-07-26 13:58:52,989 [INFO] scraper: odds_win: 6/6 parsed
2026-07-26 13:58:52,990 [INFO] scraper: fetch_race 06/6: boats=6 odds=189/191
2026-07-26 13:58:52,995 [INFO] predictor: CALIBRATION_MODE=on
2026-07-26 13:58:52,995 [INFO] predictor: combos: {'win': 6, '2t': 29, '3t': 120}
2026-07-26 13:58:53,000 [INFO] run_cycle: fetched 06/6 [scan]: 155 combos
2026-07-26 13:58:53,281 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-26 13:59:04,017 [INFO] run_cycle: === run_cycle 13:59:04 ===
2026-07-26 13:59:04,017 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-26 13:59:04,017 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-26 13:59:04,055 [INFO] predictor: Models loaded OK
2026-07-26 13:59:15,529 [INFO] scraper: odds3t: 120/120 parsed
2026-07-26 13:59:16,631 [INFO] scraper: odds3f: 20/20 parsed
2026-07-26 13:59:17,794 [INFO] scraper: odds2t: 30/30 parsed
2026-07-26 13:59:17,795 [INFO] scraper: odds2f: 15/15 parsed
2026-07-26 13:59:18,886 [INFO] scraper: odds_win: 6/6 parsed
2026-07-26 13:59:18,886 [INFO] scraper: fetch_race 23/12: boats=6 odds=191/191
2026-07-26 13:59:18,889 [INFO] predictor: CALIBRATION_MODE=on
2026-07-26 13:59:18,890 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-26 13:59:18,893 [INFO] run_cycle: fetched 23/12 [scan]: 156 combos
2026-07-26 13:59:19,081 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 72
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 72
  }
]
```

## Phase別通知記録 (24h)
{'final': 31, 'result': 13, 'scan': 28}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 200
  FINAL_MISSING: 41
  CIRCUIT_BREAKER_NO_ACTION: 30
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 11
  ANOMALY_SCAN_FINAL_RATIO: 6
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 9 | 12,600 | 8,490 | -4,110 | 0.674 |
| S01_NAKAANA1 | 35 | 5 | 7,000 | 4,460 | -2,540 | 0.637 |
| S02_TETSUBAN | 15 | 8 | 3,000 | 2,720 | -280 | 0.907 |

## 直近アラート (24h・新しい順)
```
[13:59:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1214}
[13:56:25] FINAL_MISSING: {"deadline": "2026-07-26T09:24:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072621030924", "sid": "S00"}
[13:56:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1222}
[13:55:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1224}
[13:54:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1205}
[13:53:50] FINAL_MISSING: {"deadline": "2026-07-26T13:23:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072604041323", "sid": "S00"}
[13:53:50] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1196}
[13:51:51] CIRCUIT_BREAKER_TRIP: {"cost": 12600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 42, "payout": 8490, "roi_7d": 0.674, "sid": "S00"}
[13:51:51] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1200}
[13:50:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1165}
```

## 本日残レース: 76件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 80件 締切済
- 通知発射: scan=12 nid / final=13 nid / result=3 nid
- predictions: 7 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 037R | win | 1 | 0.5174 | 2.1 | 1.09 | 200 | scan=- drift=- | 13:53:42 |
| S02_TETSUBAN | 138R | win | 1 | 0.6037 | 2.6 | 1.57 | 200 | scan=- drift=- | 13:51:29 |
| S01_NAKAANA1 | 065R | win | 1 | 0.4989 | 3.5 | 1.75 | 200 | scan=- drift=- | 13:35:19 |
| S01_NAKAANA1 | 219R | win | 1 | 0.4111 | 3.3 | 1.36 | 200 | scan=- drift=- | 12:13:18 |
| S01_NAKAANA1 | 218R | win | 1 | 0.4111 | 4.1 | 1.69 | 200 | scan=- drift=- | 11:41:18 |
| S00 | 218R | win | 1 | 0.4111 | 5.3 | 2.18 | 300 | scan=6.0 drift=-11.7% | 11:40:31 |
| S00 | 147R | win | 1 | 0.5174 | 18.0 | 9.31 | 300 | scan=- drift=- | 11:25:38 |
| S00 | 015R | win | 1 | 0.1231 | 8.0 | 0.98 | 300 | scan=- drift=- | 17:22:30 |
| S01_NAKAANA1 | 204R | win | 1 | 0.5174 | 4.2 | 2.17 | 200 | scan=3.6 drift=+16.7% | 17:10:21 |
| S00 | 204R | win | 1 | 0.5174 | 4.2 | 2.17 | 300 | scan=4.0 drift=+5.0% | 17:10:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 43 | +4.5% | -86.1% | +198.5% | 17 | 9 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 489.2s |
| **Latency** (scan→final max) | 656.1s |
| **Traffic** (notifications 24h) | 72 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 423 | 0.4627 | 0.3144 | +0.1482 | 🟡+32% | 0.2323 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 182 | 0.4187 | 0.2802 | 0.2212 | 🔴-0.10 | 0.749 |
| S01_NAKAANA1 | win | 164 | 0.4749 | 0.2622 | 0.2355 | 🔴-0.22 | 0.736 |
| S02_TETSUBAN | win | 77 | 0.5404 | 0.5065 | 0.2517 | 🔴-0.01 | 0.996 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 7 | 0.1262 | 0.1429 | ✅-0.0167 |
| 0.15-0.20 | 9 | 0.1804 | 0.3333 | 🔴-0.1530 |
| 0.20-0.30 | 13 | 0.2273 | 0.3077 | 🔴-0.0804 |
| 0.30-0.50 | 168 | 0.4147 | 0.2679 | 🔴+0.1469 |
| 0.50+ | 222 | 0.5415 | 0.3604 | 🔴+0.1812 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 85 | 0.807 |
| win | <5.0 | ✅learned | 152 | 0.725 |
| win | <10.0 | ✅learned | 81 | 0.457 |
| win | <20.0 | ✅learned | 26 | 0.216 |
| win | <50.0 | ⚠️fallback | 6 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-07-26T14:00:02.165871+09:00_