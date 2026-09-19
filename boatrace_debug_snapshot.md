# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-19T12:10:01.779540+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×43 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×88 (24h)
- 🔴 PSI_DRIFT_DETECTED×43 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×4  [2026-09-19T12:06:19]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×9  [2026-09-19T12:01:45]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×9  [2026-09-19T12:01:45]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×9  [2026-09-19T12:01:45]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×9  [2026-09-19T12:01:45]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-19T12:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×27  [2026-09-19T11:12:34]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-19T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=76<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-19T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=175<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-19T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=169<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-19T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1314 actual=0.0000 gap=+0.1314`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-19T06:00:19]
- key: `ROI_STAT|S00: n=175 hit%=24.6% hit_CI[Bonf]=[16.5,35.0]% ROI=0.76 ROI_boot95=[0.54,1.02]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-19T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=169 hit%=24.3% hit_CI[Bonf]=[16.1,34.8]% ROI=0.70 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-19T06:00:19]
- key: `ROI_STAT|S02_TETSUBAN: n=76 hit%=40.8% hit_CI[Bonf]=[26.2,57.2]% ROI=0.76 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-09-19T06:00:19]
- key: `ORPHAN_SCAN|177 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-19T06:00:19]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=30.3% ROI=0.88 (コスト 9,500/回収 8,390)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-19T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=44 hit%=20.5% ROI=0.55 (コスト 10,200/回収 5,560)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-19T06:00:19]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=81 hit%=22.2% ROI=0.68 (コスト 18,800/回収 12,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-19T06:00:19]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=45 hit%=24.4% ROI=0.51 (コスト 9,800/回収 5,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-19T06:00:19]
- key: `DRIFT_BUCKET|drift ≥+30%: n=42 hit%=11.9% ROI=0.43 (コスト 11,500/回収 4,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.61MB / last modified 2026-09-19T12:09:20.122545+09:00

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
 parsed
2026-09-19 12:07:36,725 [INFO] scraper: odds2t: 29/30 parsed
2026-09-19 12:07:36,726 [INFO] scraper: odds2f: 15/15 parsed
2026-09-19 12:07:37,889 [INFO] scraper: odds_win: 1/6 parsed
2026-09-19 12:07:37,890 [INFO] scraper: fetch_race 16/4: boats=6 odds=185/191
2026-09-19 12:07:37,892 [INFO] predictor: CALIBRATION_MODE=on
2026-09-19 12:07:37,893 [INFO] predictor: combos: {'win': 1, '2t': 29, '3t': 120}
2026-09-19 12:07:37,897 [INFO] run_cycle: fetched 16/4 [scan]: 150 combos
2026-09-19 12:07:38,148 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-19 12:08:05,033 [INFO] run_cycle: === run_cycle 12:08:05 ===
2026-09-19 12:08:05,033 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-19 12:08:05,033 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-19 12:08:05,079 [INFO] predictor: Models loaded OK
2026-09-19 12:08:05,493 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-19 12:09:03,962 [INFO] run_cycle: === run_cycle 12:09:03 ===
2026-09-19 12:09:03,962 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-19 12:09:03,962 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-19 12:09:04,031 [INFO] predictor: Models loaded OK
2026-09-19 12:09:15,922 [INFO] scraper: odds3t: 120/120 parsed
2026-09-19 12:09:16,995 [INFO] scraper: odds3f: 20/20 parsed
2026-09-19 12:09:18,127 [INFO] scraper: odds2t: 30/30 parsed
2026-09-19 12:09:18,128 [INFO] scraper: odds2f: 15/15 parsed
2026-09-19 12:09:19,230 [INFO] scraper: odds_win: 6/6 parsed
2026-09-19 12:09:19,230 [INFO] scraper: fetch_race 04/4: boats=6 odds=191/191
2026-09-19 12:09:19,233 [INFO] predictor: CALIBRATION_MODE=on
2026-09-19 12:09:19,233 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-19 12:09:19,237 [INFO] run_cycle: fetched 04/4 [scan]: 156 combos
2026-09-19 12:09:19,375 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 63
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 63
  }
]
```

## Phase別通知記録 (24h)
{'final': 24, 'result': 13, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 248
  FINAL_MISSING: 88
  PSI_DRIFT_DETECTED: 43
  CIRCUIT_BREAKER_TRIP: 22
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 7
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 9 | 12,600 | 7,950 | -4,650 | 0.631 |
| S01_NAKAANA1 | 32 | 11 | 6,400 | 7,700 | +1,300 | 1.203 |
| S02_TETSUBAN | 17 | 9 | 3,400 | 3,600 | +200 | 1.059 |

## 直近アラート (24h・新しい順)
```
[12:09:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1220}
[12:07:38] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 327, "n_recent": 91, "psi": 0.449}
[12:07:38] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1219}
[12:06:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1231}
[12:05:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1234}
[12:03:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1220}
[12:02:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1223}
[12:01:45] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:01:45] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[12:01:45] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1218}
```

## 本日残レース: 114件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 42件 締切済
- 通知発射: scan=9 nid / final=8 nid / result=4 nid
- predictions: 6 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 054R | win | 1 | 0.5123 | 2.1 | 1.08 | 200 | scan=- drift=- | 11:54:44 |
| S00 | 032R | win | 1 | 0.5334 | 5.6 | 2.99 | 300 | scan=4.8 drift=+16.7% | 11:38:31 |
| S00 | 173R | win | 1 | 0.4111 | 6.6 | 2.71 | 300 | scan=36.1 drift=-81.7% | 11:34:20 |
| S02_TETSUBAN | 053R | win | 1 | 0.5083 | 2.5 | 1.27 | 200 | scan=2.1 drift=+19.0% | 11:24:30 |
| S01_NAKAANA1 | 145R | win | 1 | 0.5735 | 3.8 | 2.18 | 200 | scan=- drift=- | 10:13:18 |
| S01_NAKAANA1 | 234R | win | 1 | 0.4111 | 4.0 | 1.64 | 200 | scan=- drift=- | 09:59:31 |
| S00 | 156R | win | 1 | 0.5259 | 6.5 | 3.42 | 300 | scan=7.1 drift=-8.5% | 17:31:43 |
| S02_TETSUBAN | 1111R | win | 1 | 0.5476 | 2.8 | 1.53 | 200 | scan=- drift=- | 15:30:45 |
| S02_TETSUBAN | 059R | win | 1 | 0.3177 | 2.9 | 0.92 | 200 | scan=2.2 drift=+31.8% | 14:35:32 |
| S00 | 168R | win | 1 | 0.5719 | 6.0 | 3.43 | 300 | scan=- drift=- | 14:19:32 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 55 | +3.0% | -81.7% | +119.5% | 14 | 5 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 435.5s |
| **Latency** (scan→final max) | 610.1s |
| **Traffic** (notifications 24h) | 63 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 416 | 0.4784 | 0.2668 | +0.2116 | 🟡+44% | 0.2410 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 172 | 0.4413 | 0.2384 | 0.2262 | 🔴-0.25 | 0.745 |
| S01_NAKAANA1 | win | 170 | 0.4886 | 0.2353 | 0.2459 | 🔴-0.37 | 0.685 |
| S02_TETSUBAN | win | 74 | 0.5413 | 0.4054 | 0.2645 | 🔴-0.10 | 0.749 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1314 | 0.0000 | 🔴+0.1314 |
| 0.30-0.50 | 149 | 0.4095 | 0.2215 | 🔴+0.1880 |
| 0.50+ | 248 | 0.5453 | 0.3065 | 🔴+0.2388 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 144 | 0.775 |
| win | <5.0 | ✅learned | 256 | 0.761 |
| win | <10.0 | ✅learned | 124 | 0.461 |
| win | <20.0 | ✅learned | 33 | 0.234 |
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
_auto-generated by claude_snapshot.py at 2026-09-19T12:10:01.779540+09:00_