# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-03T12:20:01.755978+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×46 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×15 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×17  [2026-08-03T12:03:20]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×17  [2026-08-03T12:03:20]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×17  [2026-08-03T12:03:20]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-03T11:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×38  [2026-08-03T11:22:06]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×16  [2026-08-03T11:12:27]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-08-03T11:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×15  [2026-08-03T10:00:42]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-03T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=75<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-03T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=178<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-03T06:00:07]
- key: `ORPHAN_SCAN|172 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-03T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=31 pred=0.3238 actual=0.1613 gap=+0.1625`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-03T06:00:07]
- key: `DRIFT_BUCKET|drift ≤-30%: n=32 hit%=28.1% ROI=0.67 (コスト 9,400/回収 6,300)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-03T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=10 pred=0.1241 actual=0.2000 gap=-0.0759`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-03T06:00:07]
- key: `ROI_STAT|S00: n=178 hit%=27.0% hit_CI[Bonf]=[18.6,37.4]% ROI=0.72 ROI_boot95=[0.51,0.97]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-03T06:00:07]
- key: `ROI_STAT|S01_NAKAANA1: n=164 hit%=25.6% hit_CI[Bonf]=[17.1,36.5]% ROI=0.76 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-03T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-03T06:00:07]
- key: `ROI_STAT|S02_TETSUBAN: n=75 hit%=50.7% hit_CI[Bonf]=[34.8,66.4]% ROI=0.99 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-03T06:00:07]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=38 hit%=36.8% ROI=0.87 (コスト 9,400/回収 8,160)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-03T06:00:07]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=68 hit%=32.4% ROI=0.78 (コスト 15,800/回収 12,310)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 9.31MB / last modified 2026-08-03T12:19:43.144439+09:00

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
&hd=20260803: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-03 12:19:25,886 [INFO] scraper: odds3t: 120/120 parsed
2026-08-03 12:19:26,991 [INFO] scraper: odds3f: 20/20 parsed
2026-08-03 12:19:28,091 [INFO] scraper: odds2t: 30/30 parsed
2026-08-03 12:19:28,093 [INFO] scraper: odds2f: 15/15 parsed
2026-08-03 12:19:29,196 [INFO] scraper: odds_win: 5/6 parsed
2026-08-03 12:19:29,196 [INFO] scraper: fetch_race 22/1: boats=6 odds=190/191
2026-08-03 12:19:29,199 [INFO] predictor: CALIBRATION_MODE=on
2026-08-03 12:19:29,199 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-03 12:19:29,203 [INFO] run_cycle: fetched 22/1 [final]: 155 combos
2026-08-03 12:19:32,715 [INFO] scraper: odds3t: 120/120 parsed
2026-08-03 12:19:33,857 [INFO] scraper: odds3f: 20/20 parsed
2026-08-03 12:19:34,964 [INFO] scraper: odds2t: 30/30 parsed
2026-08-03 12:19:34,965 [INFO] scraper: odds2f: 15/15 parsed
2026-08-03 12:19:36,063 [INFO] scraper: odds_win: 4/6 parsed
2026-08-03 12:19:36,063 [INFO] scraper: fetch_race 23/9: boats=6 odds=189/191
2026-08-03 12:19:36,065 [INFO] predictor: CALIBRATION_MODE=on
2026-08-03 12:19:36,065 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-08-03 12:19:36,069 [INFO] run_cycle: fetched 23/9 [scan]: 154 combos
2026-08-03 12:19:39,526 [INFO] scraper: odds3t: 120/120 parsed
2026-08-03 12:19:40,596 [INFO] scraper: odds3f: 20/20 parsed
2026-08-03 12:19:41,673 [INFO] scraper: odds2t: 26/30 parsed
2026-08-03 12:19:41,674 [INFO] scraper: odds2f: 12/15 parsed
2026-08-03 12:19:42,774 [INFO] scraper: odds_win: 3/6 parsed
2026-08-03 12:19:42,775 [INFO] scraper: fetch_race 13/5: boats=6 odds=181/191
2026-08-03 12:19:42,777 [INFO] predictor: CALIBRATION_MODE=on
2026-08-03 12:19:42,777 [INFO] predictor: combos: {'win': 3, '2t': 26, '3t': 120}
2026-08-03 12:19:42,781 [INFO] run_cycle: fetched 13/5 [scan]: 149 combos
2026-08-03 12:19:42,986 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 68
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 68
  }
]
```

## Phase別通知記録 (24h)
{'final': 28, 'result': 10, 'scan': 30}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 121
  FINAL_MISSING: 46
  CIRCUIT_BREAKER_TRIP: 22
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 15
  ANOMALY_SCAN_FINAL_RATIO: 12
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 8 | 10,500 | 6,360 | -4,140 | 0.606 |
| S01_NAKAANA1 | 35 | 10 | 7,000 | 6,700 | -300 | 0.957 |
| S02_TETSUBAN | 17 | 8 | 3,400 | 2,400 | -1,000 | 0.706 |

## 直近アラート (24h・新しい順)
```
[12:18:35] CIRCUIT_BREAKER_TRIP: {"cost": 10500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 6360, "roi_7d": 0.606, "sid": "S00"}
[12:17:04] FINAL_MISSING: {"deadline": "2026-08-03T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080321061047", "sid": "S00"}
[12:03:19] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:03:19] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[11:59:18] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1007}
[11:58:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 999}
[11:57:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1013}
[11:56:56] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1011}
[11:55:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 999}
[11:54:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1004}
```

## 本日残レース: 109件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 35件 締切済
- 通知発射: scan=11 nid / final=9 nid / result=5 nid
- predictions: 5 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 218R | win | 1 | 0.4989 | 3.7 | 1.85 | 200 | scan=3.0 drift=+23.3% | 11:44:18 |
| S01_NAKAANA1 | 173R | win | 1 | 0.5113 | 3.7 | 1.89 | 200 | scan=- drift=- | 11:43:30 |
| S00 | 133R | win | 1 | 0.1371 | 4.7 | 0.64 | 300 | scan=7.5 drift=-37.3% | 11:18:18 |
| S00 | 132R | win | 1 | 0.1957 | 8.6 | 1.68 | 300 | scan=22.1 drift=-61.1% | 10:55:20 |
| S02_TETSUBAN | 215R | win | 1 | 0.5401 | 2.6 | 1.40 | 200 | scan=2.5 drift=+4.0% | 10:15:31 |
| S00 | 2010R | win | 1 | 0.1760 | 4.2 | 0.74 | 300 | scan=- drift=- | 19:47:19 |
| S02_TETSUBAN | 1311R | win | 1 | 0.5174 | 2.7 | 1.40 | 200 | scan=- drift=- | 15:43:32 |
| S00 | 165R | win | 1 | 0.5891 | 6.0 | 3.53 | 300 | scan=6.0 drift=+0.0% | 14:01:29 |
| S02_TETSUBAN | 137R | win | 1 | 0.5891 | 2.2 | 1.30 | 200 | scan=2.8 drift=-21.4% | 13:31:19 |
| S00 | 053R | win | 1 | 0.4111 | 11.6 | 4.77 | 300 | scan=10.2 drift=+13.7% | 12:23:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 56 | +14.3% | -65.9% | +375.6% | 16 | 10 | 41 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 508.0s |
| **Latency** (scan→final max) | 611.4s |
| **Traffic** (notifications 24h) | 68 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 417 | 0.4610 | 0.3022 | +0.1589 | 🟡+34% | 0.2323 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 177 | 0.4179 | 0.2599 | 0.2247 | 🔴-0.17 | 0.71 |
| S01_NAKAANA1 | win | 164 | 0.4753 | 0.2500 | 0.2346 | 🔴-0.25 | 0.748 |
| S02_TETSUBAN | win | 76 | 0.5308 | 0.5132 | 0.2451 | ✅+0.02 | 0.987 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 11 | 0.1253 | 0.1818 | 🔴-0.0565 |
| 0.15-0.20 | 9 | 0.1808 | 0.2222 | ✅-0.0414 |
| 0.20-0.30 | 10 | 0.2244 | 0.4000 | 🔴-0.1756 |
| 0.30-0.50 | 167 | 0.4189 | 0.2335 | 🔴+0.1853 |
| 0.50+ | 216 | 0.5403 | 0.3657 | 🔴+0.1746 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 94 | 0.788 |
| win | <5.0 | ✅learned | 166 | 0.724 |
| win | <10.0 | ✅learned | 87 | 0.452 |
| win | <20.0 | ✅learned | 27 | 0.218 |
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
_auto-generated by claude_snapshot.py at 2026-08-03T12:20:01.755978+09:00_