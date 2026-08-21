# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-21T13:50:02.277578+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×22 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×48 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×46  [2026-08-21T13:04:28]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×46  [2026-08-21T13:04:28]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×46  [2026-08-21T13:04:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×61  [2026-08-21T12:49:40]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×5  [2026-08-21T12:43:32]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-21T12:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-21T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=79<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-21T06:00:13]
- key: `ORPHAN_SCAN|194 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-21T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=9 pred=0.1189 actual=0.1111 gap=+0.0078`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-21T06:00:13]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=48 hit%=25.0% ROI=0.49 (コスト 11,100/回収 5,420)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-21T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2255 actual=0.3000 gap=-0.0745`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-21T06:00:13]
- key: `ROI_STAT|S00: n=170 hit%=26.5% hit_CI[Bonf]=[18.0,37.2]% ROI=0.81 ROI_boot95=[0.55,1.09]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-21T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=170<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-21T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=175 hit%=26.3% hit_CI[Bonf]=[17.9,36.8]% ROI=0.89 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-21T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=175<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-21T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=79 hit%=45.6% hit_CI[Bonf]=[30.6,61.4]% ROI=0.72 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-21T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=37 hit%=24.3% ROI=0.69 (コスト 10,700/回収 7,400)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-21T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=37 hit%=37.8% ROI=1.14 (コスト 8,800/回収 10,050)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-21T06:00:13]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=91 hit%=27.5% ROI=0.87 (コスト 21,100/回収 18,410)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-21T06:00:13]
- key: `DRIFT_BUCKET|drift ≥+30%: n=35 hit%=25.7% ROI=1.21 (コスト 9,700/回収 11,710)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.05MB / last modified 2026-08-21T13:49:29.640007+09:00

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
run_cycle done: 0 notifications
2026-08-21 13:49:04,432 [INFO] run_cycle: === run_cycle 13:49:04 ===
2026-08-21 13:49:04,432 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-21 13:49:04,432 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-21 13:49:04,479 [INFO] predictor: Models loaded OK
2026-08-21 13:49:17,173 [INFO] scraper: odds3t: 120/120 parsed
2026-08-21 13:49:18,294 [INFO] scraper: odds3f: 20/20 parsed
2026-08-21 13:49:19,364 [INFO] scraper: odds2t: 30/30 parsed
2026-08-21 13:49:19,365 [INFO] scraper: odds2f: 15/15 parsed
2026-08-21 13:49:20,474 [INFO] scraper: odds_win: 6/6 parsed
2026-08-21 13:49:20,474 [INFO] scraper: fetch_race 04/5: boats=6 odds=191/191
2026-08-21 13:49:20,478 [INFO] predictor: CALIBRATION_MODE=on
2026-08-21 13:49:20,478 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-21 13:49:20,482 [INFO] run_cycle: fetched 04/5 [scan]: 156 combos
2026-08-21 13:49:24,011 [INFO] scraper: odds3t: 120/120 parsed
2026-08-21 13:49:25,111 [INFO] scraper: odds3f: 20/20 parsed
2026-08-21 13:49:26,314 [INFO] scraper: odds2t: 30/30 parsed
2026-08-21 13:49:26,315 [INFO] scraper: odds2f: 15/15 parsed
2026-08-21 13:49:27,506 [INFO] scraper: odds_win: 6/6 parsed
2026-08-21 13:49:27,507 [INFO] scraper: fetch_race 03/7: boats=6 odds=191/191
2026-08-21 13:49:27,509 [INFO] predictor: CALIBRATION_MODE=on
2026-08-21 13:49:27,509 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-21 13:49:27,513 [INFO] run_cycle: fetched 03/7 [scan]: 156 combos
2026-08-21 13:49:27,732 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-21 13:50:04,921 [INFO] run_cycle: === run_cycle 13:50:04 ===
2026-08-21 13:50:04,922 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-21 13:50:04,922 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-21 13:50:04,971 [INFO] predictor: Models loaded OK

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
    "c": 70
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 70
  }
]
```

## Phase別通知記録 (24h)
{'final': 30, 'result': 19, 'scan': 21}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 159
  FINAL_MISSING: 48
  CIRCUIT_BREAKER_TRIP: 22
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 4
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 41 | 15 | 12,300 | 16,950 | +4,650 | 1.378 |
| S01_NAKAANA1 | 48 | 19 | 9,600 | 13,000 | +3,400 | 1.354 |
| S02_TETSUBAN | 27 | 7 | 5,400 | 2,280 | -3,120 | 0.422 |

## 直近アラート (24h・新しい順)
```
[13:49:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1015}
[13:47:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1030}
[13:46:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1025}
[13:45:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1007}
[13:44:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1028}
[13:43:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1026}
[13:42:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1009}
[13:41:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1011}
[13:40:38] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1002}
[13:39:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 992}
```

## 本日残レース: 87件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 57件 締切済
- 通知発射: scan=8 nid / final=13 nid / result=10 nid
- predictions: 12 / うち結果DB記録済: 10
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 065R | win | 1 | 0.5891 | 4.3 | 2.53 | 200 | scan=3.0 drift=+43.3% | 13:34:20 |
| S00 | 044R | win | 1 | 0.1371 | 15.5 | 2.13 | 300 | scan=22.5 drift=-31.1% | 13:21:19 |
| S02_TETSUBAN | 2110R | win | 1 | 0.5891 | 2.6 | 1.53 | 200 | scan=2.2 drift=+18.2% | 12:54:30 |
| S02_TETSUBAN | 136R | win | 1 | 0.5891 | 2.6 | 1.53 | 200 | scan=2.8 drift=-7.1% | 12:48:18 |
| S01_NAKAANA1 | 034R | win | 1 | 0.5735 | 4.2 | 2.41 | 200 | scan=- drift=- | 12:33:31 |
| S01_NAKAANA1 | 024R | win | 1 | 0.4111 | 4.6 | 1.89 | 200 | scan=4.1 drift=+12.2% | 12:11:32 |
| S00 | 164R | win | 1 | 0.4111 | 5.4 | 2.22 | 300 | scan=- drift=- | 12:03:21 |
| S00 | 134R | win | 1 | 0.6037 | 4.0 | 2.41 | 300 | scan=- drift=- | 11:49:20 |
| S02_TETSUBAN | 133R | win | 1 | 0.5735 | 2.1 | 1.20 | 200 | scan=- drift=- | 11:24:45 |
| S00 | 217R | win | 1 | 0.1485 | 7.8 | 1.16 | 300 | scan=5.1 drift=+52.9% | 11:18:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 71 | +4.0% | -56.0% | +256.4% | 19 | 8 | 37 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 445.1s |
| **Latency** (scan→final max) | 610.8s |
| **Traffic** (notifications 24h) | 70 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 427 | 0.4679 | 0.2998 | +0.1681 | 🟡+36% | 0.2395 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 172 | 0.4148 | 0.2674 | 0.2233 | 🔴-0.14 | 0.815 |
| S01_NAKAANA1 | win | 173 | 0.4891 | 0.2659 | 0.2500 | 🔴-0.28 | 0.859 |
| S02_TETSUBAN | win | 82 | 0.5343 | 0.4390 | 0.2516 | 🔴-0.02 | 0.691 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1219 | 0.1000 | ✅+0.0219 |
| 0.15-0.20 | 12 | 0.1800 | 0.1667 | ✅+0.0134 |
| 0.20-0.30 | 10 | 0.2255 | 0.3000 | 🔴-0.0745 |
| 0.30-0.50 | 151 | 0.4119 | 0.2517 | 🔴+0.1603 |
| 0.50+ | 242 | 0.5446 | 0.3471 | 🔴+0.1975 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 115 | 0.769 |
| win | <5.0 | ✅learned | 209 | 0.752 |
| win | <10.0 | ✅learned | 101 | 0.456 |
| win | <20.0 | ✅learned | 30 | 0.227 |
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
_auto-generated by claude_snapshot.py at 2026-08-21T13:50:02.277578+09:00_