# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-17T11:40:01.832465+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×45 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×5  [2026-10-17T11:35:13]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-17T11:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-17T11:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-10-17T11:17:27]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×70  [2026-10-17T11:03:50]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×35  [2026-10-17T11:03:50]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-10-17T10:00:09]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ORPHAN_SCAN  ×1  [2026-10-17T06:00:26]
- key: `ORPHAN_SCAN|157 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-17T06:00:26]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=86<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-17T06:00:26]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=170<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-17T06:00:26]
- key: `INSUFFICIENT_SAMPLE|S00: n=180<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-17T06:00:26]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=6 pred=0.2287 actual=0.3333 gap=-0.1046`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-17T06:00:26]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=34 pred=0.3223 actual=0.2353 gap=+0.0870`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-17T06:00:26]
- key: `ROI_STAT|S00: n=180 hit%=27.8% hit_CI[Bonf]=[19.3,38.2]% ROI=0.75 ROI_boot95=[0.55,0.98]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-17T06:00:26]
- key: `ROI_STAT|S01_NAKAANA1: n=170 hit%=35.9% hit_CI[Bonf]=[26.2,46.9]% ROI=1.03 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-17T06:00:26]
- key: `ROI_STAT|S02_TETSUBAN: n=86 hit%=53.5% hit_CI[Bonf]=[38.4,68.0]% ROI=0.95 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-17T06:00:26]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=42.4% ROI=1.07 (コスト 9,500/回収 10,170)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-17T06:00:26]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=48 hit%=33.3% ROI=0.77 (コスト 11,300/回収 8,720)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-17T06:00:26]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=87 hit%=40.2% ROI=1.19 (コスト 19,800/回収 23,500)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-17T06:00:26]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=59 hit%=35.6% ROI=0.90 (コスト 14,200/回収 12,820)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.02MB / last modified 2026-10-17T11:39:19.893779+09:00

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
rsed
2026-10-17 11:38:25,894 [INFO] scraper: fetch_race 08/4: boats=6 odds=184/191
2026-10-17 11:38:25,897 [INFO] predictor: CALIBRATION_MODE=on
2026-10-17 11:38:25,897 [INFO] predictor: combos: {'win': 4, '2t': 26, '3t': 120}
2026-10-17 11:38:25,901 [INFO] run_cycle: fetched 08/4 [scan]: 150 combos
2026-10-17 11:38:29,486 [INFO] scraper: odds3t: 120/120 parsed
2026-10-17 11:38:30,625 [INFO] scraper: odds3f: 20/20 parsed
2026-10-17 11:38:31,790 [INFO] scraper: odds2t: 30/30 parsed
2026-10-17 11:38:31,791 [INFO] scraper: odds2f: 15/15 parsed
2026-10-17 11:38:32,859 [INFO] scraper: odds_win: 5/6 parsed
2026-10-17 11:38:32,859 [INFO] scraper: fetch_race 02/3: boats=6 odds=190/191
2026-10-17 11:38:32,862 [INFO] predictor: CALIBRATION_MODE=on
2026-10-17 11:38:32,862 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-10-17 11:38:32,866 [INFO] run_cycle: fetched 02/3 [scan]: 155 combos
2026-10-17 11:38:33,100 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-17 11:39:04,550 [INFO] run_cycle: === run_cycle 11:39:04 ===
2026-10-17 11:39:04,550 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-17 11:39:04,550 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-17 11:39:04,603 [INFO] predictor: Models loaded OK
2026-10-17 11:39:16,056 [INFO] scraper: odds3t: 120/120 parsed
2026-10-17 11:39:17,133 [INFO] scraper: odds3f: 20/20 parsed
2026-10-17 11:39:18,224 [INFO] scraper: odds2t: 29/30 parsed
2026-10-17 11:39:18,225 [INFO] scraper: odds2f: 15/15 parsed
2026-10-17 11:39:19,304 [INFO] scraper: odds_win: 4/6 parsed
2026-10-17 11:39:19,304 [INFO] scraper: fetch_race 03/2: boats=6 odds=188/191
2026-10-17 11:39:19,307 [INFO] predictor: CALIBRATION_MODE=on
2026-10-17 11:39:19,308 [INFO] predictor: combos: {'win': 4, '2t': 29, '3t': 120}
2026-10-17 11:39:19,311 [INFO] run_cycle: fetched 03/2 [final]: 153 combos
2026-10-17 11:39:19,694 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 24, 'result': 18, 'scan': 21}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 247
  FINAL_MISSING: 45
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 7
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 1
  CIRCUIT_BREAKER_TRIP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 53 | 15 | 15,900 | 14,130 | -1,770 | 0.889 |
| S01_NAKAANA1 | 41 | 15 | 8,200 | 6,840 | -1,360 | 0.834 |
| S02_TETSUBAN | 22 | 13 | 4,400 | 4,760 | +360 | 1.082 |

## 直近アラート (24h・新しい順)
```
[11:39:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1247}
[11:38:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1237}
[11:37:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1230}
[11:36:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1240}
[11:35:09] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1227}
[11:27:28] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": -25.3, "final": 5.6, "kind": "LARGE_ODDS_DRIFT", "race": "093R", "scan": 7.5, "sid": "S00"}
[11:25:20] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.377, "baseline_mean": 0.877, "baseline_stdev": 0.072, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 4, "z_score": -5.24}
[11:18:21] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.21, "baseline_mean": 0.877, "baseline_stdev": 0.072, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 3, "z_score": -2.92}
[11:17:27] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.544, "baseline_mean": 0.877, "baseline_stdev": 0.072, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.333, "today_scan_count": 3, "z_score": -7.56}
[11:03:50] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 130件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 38件 締切済
- 通知発射: scan=4 nid / final=4 nid / result=0 nid
- predictions: 1 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 093R | win | 1 | 0.4111 | 5.6 | 2.30 | 300 | scan=7.5 drift=-25.3% | 11:27:19 |
| S02_TETSUBAN | 202R | win | 1 | 0.5735 | 2.7 | 1.55 | 200 | scan=- drift=- | 15:47:20 |
| S02_TETSUBAN | 0310R | win | 1 | 0.5735 | 2.0 | 1.15 | 200 | scan=- drift=- | 15:19:29 |
| S01_NAKAANA1 | 038R | win | 1 | 0.5031 | 4.0 | 2.01 | 200 | scan=- drift=- | 14:21:19 |
| S00 | 098R | win | 1 | 0.1957 | 5.0 | 0.98 | 300 | scan=- drift=- | 13:58:20 |
| S01_NAKAANA1 | 037R | win | 1 | 0.4989 | 4.7 | 2.34 | 200 | scan=4.7 drift=+0.0% | 13:53:20 |
| S01_NAKAANA1 | 026R | win | 1 | 0.5073 | 4.5 | 2.28 | 200 | scan=3.3 drift=+36.4% | 13:11:22 |
| S00 | 026R | win | 1 | 0.5073 | 4.5 | 2.28 | 300 | scan=7.1 drift=-36.6% | 13:11:20 |
| S00 | 035R | win | 1 | 0.4922 | 5.2 | 2.56 | 300 | scan=4.5 drift=+15.6% | 12:59:26 |
| S00 | 096R | win | 1 | 0.4989 | 8.8 | 4.39 | 300 | scan=6.0 drift=+46.7% | 12:53:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 71 | +17.0% | -52.2% | +326.7% | 15 | 7 | 50 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 502.6s |
| **Latency** (scan→final max) | 672.7s |
| **Traffic** (notifications 24h) | 63 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 433 | 0.4785 | 0.3580 | +0.1205 | 🟡+25% | 0.2451 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 179 | 0.4429 | 0.2793 | 0.2394 | 🔴-0.19 | 0.751 |
| S01_NAKAANA1 | win | 169 | 0.4907 | 0.3550 | 0.2445 | 🔴-0.07 | 1.022 |
| S02_TETSUBAN | win | 85 | 0.5290 | 0.5294 | 0.2585 | 🔴-0.04 | 0.933 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1269 | 0.3333 | 🔴-0.2064 |
| 0.15-0.20 | 6 | 0.1845 | 0.0000 | 🔴+0.1845 |
| 0.20-0.30 | 6 | 0.2287 | 0.3333 | 🔴-0.1046 |
| 0.30-0.50 | 159 | 0.4168 | 0.3208 | 🔴+0.0960 |
| 0.50+ | 253 | 0.5436 | 0.3913 | 🔴+0.1523 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 185 | 0.772 |
| win | <5.0 | ✅learned | 331 | 0.751 |
| win | <10.0 | ✅learned | 146 | 0.462 |
| win | <20.0 | ✅learned | 42 | 0.244 |
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
_auto-generated by claude_snapshot.py at 2026-10-17T11:40:01.832465+09:00_