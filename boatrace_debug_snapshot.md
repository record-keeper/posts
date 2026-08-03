# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-03T16:20:01.311121+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×53 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×7 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×6  [2026-08-03T16:14:19]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×12  [2026-08-03T16:07:50]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×12  [2026-08-03T16:07:50]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-03T15:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×44  [2026-08-03T15:06:21]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×28  [2026-08-03T14:52:28]
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
- DB: 9.35MB / last modified 2026-08-03T16:19:26.111224+09:00

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
d
2026-08-03 16:18:19,289 [INFO] scraper: fetch_race 19/3: boats=6 odds=190/191
2026-08-03 16:18:19,297 [INFO] predictor: CALIBRATION_MODE=on
2026-08-03 16:18:19,297 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-03 16:18:19,307 [INFO] run_cycle: fetched 19/3 [final]: 155 combos
2026-08-03 16:18:19,519 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-03 16:19:04,184 [INFO] run_cycle: === run_cycle 16:19:04 ===
2026-08-03 16:19:04,184 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-03 16:19:04,184 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-03 16:19:04,218 [INFO] predictor: Models loaded OK
2026-08-03 16:19:15,628 [INFO] scraper: odds3t: 120/120 parsed
2026-08-03 16:19:16,707 [INFO] scraper: odds3f: 20/20 parsed
2026-08-03 16:19:17,839 [INFO] scraper: odds2t: 30/30 parsed
2026-08-03 16:19:17,841 [INFO] scraper: odds2f: 15/15 parsed
2026-08-03 16:19:18,937 [INFO] scraper: odds_win: 4/6 parsed
2026-08-03 16:19:18,937 [INFO] scraper: fetch_race 22/9: boats=6 odds=189/191
2026-08-03 16:19:18,940 [INFO] predictor: CALIBRATION_MODE=on
2026-08-03 16:19:18,940 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-08-03 16:19:18,944 [INFO] run_cycle: fetched 22/9 [final]: 154 combos
2026-08-03 16:19:22,418 [INFO] scraper: odds3t: 120/120 parsed
2026-08-03 16:19:23,524 [INFO] scraper: odds3f: 20/20 parsed
2026-08-03 16:19:24,626 [INFO] scraper: odds2t: 30/30 parsed
2026-08-03 16:19:24,627 [INFO] scraper: odds2f: 15/15 parsed
2026-08-03 16:19:25,729 [INFO] scraper: odds_win: 3/6 parsed
2026-08-03 16:19:25,729 [INFO] scraper: fetch_race 06/11: boats=6 odds=188/191
2026-08-03 16:19:25,736 [INFO] predictor: CALIBRATION_MODE=on
2026-08-03 16:19:25,736 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-08-03 16:19:25,740 [INFO] run_cycle: fetched 06/11 [scan]: 153 combos
2026-08-03 16:19:25,868 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 52
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 52
  }
]
```

## Phase別通知記録 (24h)
{'final': 20, 'result': 10, 'scan': 22}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 221
  FINAL_MISSING: 53
  CIRCUIT_BREAKER_TRIP: 21
  ANOMALY_SCAN_FINAL_RATIO: 19
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 7
  ANOMALY_BET_VOLUME_DROP: 1
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 33 | 9 | 9,900 | 7,200 | -2,700 | 0.727 |
| S01_NAKAANA1 | 36 | 10 | 7,200 | 6,700 | -500 | 0.931 |
| S02_TETSUBAN | 17 | 8 | 3,400 | 2,400 | -1,000 | 0.706 |

## 直近アラート (24h・新しい順)
```
[16:19:25] FINAL_MISSING: {"deadline": "2026-08-03T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080321061047", "sid": "S00"}
[16:19:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1143}
[16:17:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1154}
[16:16:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1146}
[16:15:51] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1138}
[16:14:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1153}
[16:07:50] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[16:07:50] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[16:03:38] FINAL_MISSING: {"deadline": "2026-08-03T12:31:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080305031231", "sid": "S00"}
[15:47:51] FINAL_MISSING: {"deadline": "2026-08-03T13:15:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080317061315", "sid": "S00"}
```

## 本日残レース: 39件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 105件 締切済
- 通知発射: scan=19 nid / final=17 nid / result=9 nid
- predictions: 9 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 201R | win | 1 | 0.5123 | 11.2 | 5.74 | 300 | scan=11.2 drift=+0.0% | 15:18:19 |
| S01_NAKAANA1 | 011R | win | 1 | 0.5891 | 3.2 | 1.89 | 200 | scan=4.0 drift=-20.0% | 15:15:29 |
| S01_NAKAANA1 | 225R | win | 1 | 0.5891 | 3.2 | 1.89 | 200 | scan=- drift=- | 14:15:18 |
| S01_NAKAANA1 | 044R | win | 1 | 0.5476 | 3.3 | 1.81 | 200 | scan=- drift=- | 13:21:19 |
| S01_NAKAANA1 | 218R | win | 1 | 0.4989 | 3.7 | 1.85 | 200 | scan=3.0 drift=+23.3% | 11:44:18 |
| S01_NAKAANA1 | 173R | win | 1 | 0.5113 | 3.7 | 1.89 | 200 | scan=- drift=- | 11:43:30 |
| S00 | 133R | win | 1 | 0.1371 | 4.7 | 0.64 | 300 | scan=7.5 drift=-37.3% | 11:18:18 |
| S00 | 132R | win | 1 | 0.1957 | 8.6 | 1.68 | 300 | scan=22.1 drift=-61.1% | 10:55:20 |
| S02_TETSUBAN | 215R | win | 1 | 0.5401 | 2.6 | 1.40 | 200 | scan=2.5 drift=+4.0% | 10:15:31 |
| S00 | 2010R | win | 1 | 0.1760 | 4.2 | 0.74 | 300 | scan=- drift=- | 19:47:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 55 | +13.9% | -65.9% | +375.6% | 16 | 9 | 40 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 465.6s |
| **Latency** (scan→final max) | 623.0s |
| **Traffic** (notifications 24h) | 52 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 414 | 0.4613 | 0.2971 | +0.1642 | 🟡+36% | 0.2325 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 176 | 0.4173 | 0.2670 | 0.2243 | 🔴-0.15 | 0.73 |
| S01_NAKAANA1 | win | 164 | 0.4777 | 0.2378 | 0.2349 | 🔴-0.30 | 0.71 |
| S02_TETSUBAN | win | 74 | 0.5294 | 0.5000 | 0.2469 | ✅+0.01 | 0.964 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 11 | 0.1253 | 0.1818 | 🔴-0.0565 |
| 0.15-0.20 | 9 | 0.1808 | 0.2222 | ✅-0.0414 |
| 0.20-0.30 | 10 | 0.2244 | 0.4000 | 🔴-0.1756 |
| 0.30-0.50 | 165 | 0.4190 | 0.2242 | 🔴+0.1947 |
| 0.50+ | 215 | 0.5406 | 0.3628 | 🔴+0.1779 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 94 | 0.788 |
| win | <5.0 | ✅learned | 166 | 0.724 |
| win | <10.0 | ✅learned | 87 | 0.452 |
| win | <20.0 | ✅learned | 28 | 0.219 |
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
_auto-generated by claude_snapshot.py at 2026-08-03T16:20:01.311121+09:00_