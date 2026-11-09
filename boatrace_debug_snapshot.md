# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-09T15:50:01.930266+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×32 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×104 (24h)
- 🔴 PSI_DRIFT_DETECTED×32 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×1  [2026-11-09T15:46:06]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×14  [2026-11-09T15:15:38]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×14  [2026-11-09T15:15:38]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-09T15:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-09T14:30:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 13 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-09T14:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 10 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-09T13:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-09T12:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×2  [2026-11-09T12:05:13]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-11-09T11:15:15]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-09T11:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×17  [2026-11-09T10:00:05]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-09T09:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-09T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S00: n=147<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-09T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=151<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-11-09T06:00:08]
- key: `ORPHAN_SCAN|188 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-09T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2290 actual=0.1111 gap=+0.1179`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-09T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1878 actual=0.0000 gap=+0.1878`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-09T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=30 pred=0.3218 actual=0.1333 gap=+0.1885`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-09T06:00:08]
- key: `DRIFT_BUCKET|drift ≥+30%: n=36 hit%=16.7% ROI=0.50 (コスト 9,600/回収 4,790)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.75MB / last modified 2026-11-09T15:46:06.211988+09:00

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
': 1500} default=5000
2026-11-09 15:47:05,378 [INFO] predictor: Models loaded OK
2026-11-09 15:47:25,561 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/beforeinfo?rno=12&jcd=11&hd=20261109: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-09 15:47:46,779 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds3t?rno=12&jcd=11&hd=20261109: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-09 15:47:56,957 [INFO] scraper: odds3t: 120/120 parsed
2026-11-09 15:48:06,054 [INFO] scraper: odds3f: 20/20 parsed
2026-11-09 15:48:16,167 [INFO] scraper: odds2t: 30/30 parsed
2026-11-09 15:48:16,168 [INFO] scraper: odds2f: 15/15 parsed
2026-11-09 15:48:26,252 [INFO] scraper: odds_win: 3/6 parsed
2026-11-09 15:48:26,252 [INFO] scraper: fetch_race 11/12: boats=6 odds=188/191
2026-11-09 15:48:26,256 [INFO] predictor: CALIBRATION_MODE=on
2026-11-09 15:48:26,256 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-11-09 15:48:26,260 [INFO] run_cycle: fetched 11/12 [final]: 153 combos
2026-11-09 15:48:37,443 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=2&jcd=12&hd=20261109: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-09 15:49:06,178 [INFO] scraper: odds3t: 120/120 parsed
2026-11-09 15:49:15,266 [INFO] scraper: odds3f: 20/20 parsed
2026-11-09 15:49:25,385 [INFO] scraper: odds2t: 30/30 parsed
2026-11-09 15:49:25,386 [INFO] scraper: odds2f: 15/15 parsed
2026-11-09 15:49:35,607 [INFO] scraper: odds_win: 6/6 parsed
2026-11-09 15:49:35,607 [INFO] scraper: fetch_race 12/2: boats=6 odds=191/191
2026-11-09 15:49:35,609 [INFO] predictor: CALIBRATION_MODE=on
2026-11-09 15:49:35,609 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-11-09 15:49:35,614 [INFO] run_cycle: fetched 12/2 [scan]: 156 combos

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
    "c": 29
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 29
  }
]
```

## Phase別通知記録 (24h)
{'final': 6, 'result': 5, 'scan': 18}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 322
  FINAL_MISSING: 104
  PSI_DRIFT_DETECTED: 32
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_SCAN_FINAL_RATIO: 1
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 8 | 1 | 2,400 | 540 | -1,860 | 0.225 |
| S01_NAKAANA1 | 17 | 8 | 3,400 | 4,800 | +1,400 | 1.412 |
| S02_TETSUBAN | 10 | 4 | 2,000 | 1,320 | -680 | 0.66 |

## 直近アラート (24h・新しい順)
```
[15:46:03] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 314, "n_recent": 35, "psi": 1.408}
[15:46:03] FINAL_MISSING: {"deadline": "2026-11-09T11:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110902021112", "sid": "S00"}
[15:46:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 503}
[15:44:09] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 315, "n_recent": 35, "psi": 1.405}
[15:44:09] FINAL_MISSING: {"deadline": "2026-11-09T13:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110914061308", "sid": "S00"}
[15:44:09] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 502}
[15:40:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 498}
[15:38:34] FINAL_MISSING: {"deadline": "2026-11-09T12:02:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110921081202", "sid": "S00"}
[15:38:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 496}
[15:35:47] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 316, "n_recent": 35, "psi": 1.402}
```

## 本日残レース: 35件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 120件 登録 / 85件 締切済
- 通知発射: scan=13 nid / final=5 nid / result=3 nid
- predictions: 3 / うち結果DB記録済: 3
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 10件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 055R | win | 1 | 0.5174 | 2.8 | 1.45 | 200 | scan=2.6 drift=+7.7% | 12:22:03 |
| S00 | 085R | win | 1 | 0.5123 | 5.8 | 2.97 | 300 | scan=6.3 drift=-7.9% | 12:08:50 |
| S01_NAKAANA1 | 021R | win | 1 | 0.5334 | 4.5 | 2.40 | 200 | scan=- drift=- | 10:44:01 |
| S01_NAKAANA1 | 196R | win | 1 | 0.5123 | 4.0 | 2.05 | 200 | scan=3.4 drift=+17.6% | 17:36:24 |
| S02_TETSUBAN | 0311R | win | 1 | 0.5174 | 2.2 | 1.14 | 200 | scan=2.1 drift=+4.8% | 15:28:25 |
| S02_TETSUBAN | 057R | win | 1 | 0.5719 | 2.3 | 1.32 | 200 | scan=- drift=- | 13:20:23 |
| S00 | 087R | win | 1 | 0.0295 | 7.7 | 0.23 | 300 | scan=- drift=- | 13:05:48 |
| S00 | 083R | win | 1 | 0.3177 | 7.2 | 2.29 | 300 | scan=21.7 drift=-66.8% | 11:08:23 |
| S00 | 112R | win | 1 | 0.3177 | 8.5 | 2.70 | 300 | scan=- drift=- | 10:53:11 |
| S02_TETSUBAN | 0511R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=2.2 drift=+0.0% | 15:22:38 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 19 | -5.1% | -66.8% | +17.6% | 5 | 1 | 9 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 469.5s |
| **Latency** (scan→final max) | 649.2s |
| **Traffic** (notifications 24h) | 29 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 349 | 0.4736 | 0.3123 | +0.1613 | 🟡+34% | 0.2291 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 142 | 0.4273 | 0.2535 | 0.2078 | 🔴-0.10 | 0.666 |
| S01_NAKAANA1 | win | 147 | 0.4863 | 0.3061 | 0.2367 | 🔴-0.11 | 0.75 |
| S02_TETSUBAN | win | 60 | 0.5523 | 0.4667 | 0.2613 | 🔴-0.05 | 1.082 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1878 | 0.0000 | 🔴+0.1878 |
| 0.20-0.30 | 9 | 0.2290 | 0.1111 | 🔴+0.1179 |
| 0.30-0.50 | 128 | 0.4128 | 0.2812 | 🔴+0.1315 |
| 0.50+ | 199 | 0.5450 | 0.3618 | 🔴+0.1832 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 201 | 0.808 |
| win | <5.0 | ✅learned | 369 | 0.742 |
| win | <10.0 | ✅learned | 157 | 0.451 |
| win | <20.0 | ✅learned | 47 | 0.249 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-11-09T15:50:01.930266+09:00_