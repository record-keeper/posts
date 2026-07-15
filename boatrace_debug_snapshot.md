# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-15T12:00:01.873225+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×8 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-15T12:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×5  [2026-07-15T11:36:50]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×59  [2026-07-15T11:01:26]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×59  [2026-07-15T11:01:26]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×61  [2026-07-15T10:55:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-15T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=153<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-15T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=68<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-15T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=29 pred=0.3244 actual=0.1034 gap=+0.2210`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-15T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1777 actual=0.5714 gap=-0.3938`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-15T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=16 pred=0.2282 actual=0.1875 gap=+0.0407`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-15T06:00:08]
- key: `ROI_STAT|S00: n=173 hit%=28.9% hit_CI[Bonf]=[20.1,39.6]% ROI=0.74 ROI_boot95=[0.55,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-15T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S00: n=173<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-15T06:00:08]
- key: `ROI_STAT|S01_NAKAANA1: n=153 hit%=30.1% hit_CI[Bonf]=[20.6,41.6]% ROI=0.79 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-15T06:00:08]
- key: `ROI_STAT|S02_TETSUBAN: n=68 hit%=42.6% hit_CI[Bonf]=[27.1,59.8]% ROI=0.85 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-07-15T06:00:08]
- key: `ORPHAN_SCAN|167 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-15T06:00:08]
- key: `DRIFT_BUCKET|drift ≤-30%: n=30 hit%=33.3% ROI=0.86 (コスト 8,700/回収 7,470)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-15T06:00:08]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=45 hit%=33.3% ROI=0.78 (コスト 11,000/回収 8,580)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-15T06:00:08]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=87 hit%=31.0% ROI=0.82 (コスト 19,900/回収 16,330)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-15T06:00:08]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=36 hit%=30.6% ROI=0.60 (コスト 8,900/回収 5,370)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-15T06:00:08]
- key: `DRIFT_BUCKET|drift ≥+30%: n=31 hit%=19.4% ROI=0.41 (コスト 8,700/回収 3,570)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 7.71MB / last modified 2026-07-15T11:59:41.334718+09:00

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
2026-07-15 11:59:24,421 [INFO] scraper: odds2f: 12/15 parsed
2026-07-15 11:59:25,607 [INFO] scraper: odds_win: 3/6 parsed
2026-07-15 11:59:25,607 [INFO] scraper: fetch_race 18/8: boats=6 odds=183/191
2026-07-15 11:59:25,609 [INFO] predictor: CALIBRATION_MODE=on
2026-07-15 11:59:25,609 [INFO] predictor: combos: {'win': 3, '2t': 28, '3t': 120}
2026-07-15 11:59:25,613 [INFO] run_cycle: fetched 18/8 [final]: 151 combos
2026-07-15 11:59:29,242 [INFO] scraper: odds3t: 120/120 parsed
2026-07-15 11:59:30,338 [INFO] scraper: odds3f: 19/20 parsed
2026-07-15 11:59:31,410 [INFO] scraper: odds2t: 29/30 parsed
2026-07-15 11:59:31,411 [INFO] scraper: odds2f: 11/15 parsed
2026-07-15 11:59:32,661 [INFO] scraper: odds_win: 5/6 parsed
2026-07-15 11:59:32,661 [INFO] scraper: fetch_race 08/4: boats=6 odds=184/191
2026-07-15 11:59:32,663 [INFO] predictor: CALIBRATION_MODE=on
2026-07-15 11:59:32,663 [INFO] predictor: combos: {'win': 5, '2t': 29, '3t': 120}
2026-07-15 11:59:32,670 [INFO] run_cycle: fetched 08/4 [scan]: 154 combos
2026-07-15 11:59:32,806 [INFO] race_id: notif: nid=2026071508041206 sid=S00 phase=scan rank=A
2026-07-15 11:59:33,217 [INFO] notifier: Discord notify OK (status=204)
2026-07-15 11:59:34,020 [INFO] notifier: Discord notify OK (status=204)
2026-07-15 11:59:34,024 [INFO] run_cycle: SCAN S00 常滑4R A
2026-07-15 11:59:37,542 [INFO] scraper: odds3t: 120/120 parsed
2026-07-15 11:59:38,637 [INFO] scraper: odds3f: 20/20 parsed
2026-07-15 11:59:39,753 [INFO] scraper: odds2t: 30/30 parsed
2026-07-15 11:59:39,754 [INFO] scraper: odds2f: 15/15 parsed
2026-07-15 11:59:40,847 [INFO] scraper: odds_win: 1/6 parsed
2026-07-15 11:59:40,847 [INFO] scraper: fetch_race 03/3: boats=6 odds=186/191
2026-07-15 11:59:40,849 [INFO] predictor: CALIBRATION_MODE=on
2026-07-15 11:59:40,850 [INFO] predictor: combos: {'win': 1, '2t': 30, '3t': 120}
2026-07-15 11:59:40,853 [INFO] run_cycle: fetched 03/3 [scan]: 151 combos
2026-07-15 11:59:40,951 [INFO] run_cycle: run_cycle done: 1 notifications

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
{'final': 23, 'result': 13, 'scan': 16}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 106
  FINAL_MISSING: 21
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 8
  ANOMALY_SCAN_FINAL_RATIO: 4
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 48 | 15 | 14,400 | 12,990 | -1,410 | 0.902 |
| S01_NAKAANA1 | 39 | 13 | 7,800 | 7,000 | -800 | 0.897 |
| S02_TETSUBAN | 17 | 7 | 3,400 | 3,400 | +0 | 1.0 |

## 直近アラート (24h・新しい順)
```
[11:59:40] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.294, "baseline_mean": 0.794, "baseline_stdev": 0.081, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 4, "z_score": -3.63}
[11:55:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1126}
[11:54:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1108}
[11:53:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1099}
[11:52:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1090}
[11:51:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1080}
[11:50:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1068}
[11:49:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1066}
[11:48:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1059}
[11:47:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1051}
```

## 本日残レース: 131件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 37件 締切済
- 通知発射: scan=4 nid / final=8 nid / result=5 nid
- predictions: 7 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 134R | win | 1 | 0.1303 | 9.3 | 1.21 | 300 | scan=- drift=- | 11:58:18 |
| S01_NAKAANA1 | 238R | win | 1 | 0.4989 | 3.3 | 1.65 | 200 | scan=- drift=- | 11:51:19 |
| S00 | 082R | win | 1 | 0.4111 | 22.1 | 9.09 | 300 | scan=- drift=- | 11:05:19 |
| S01_NAKAANA1 | 186R | win | 1 | 0.5735 | 3.8 | 2.18 | 200 | scan=- drift=- | 10:56:29 |
| S01_NAKAANA1 | 081R | win | 1 | 0.5891 | 3.0 | 1.77 | 200 | scan=3.0 drift=+0.0% | 10:37:20 |
| S01_NAKAANA1 | 213R | win | 1 | 0.5735 | 4.6 | 2.64 | 200 | scan=- drift=- | 09:21:18 |
| S01_NAKAANA1 | 212R | win | 1 | 0.4889 | 3.5 | 1.71 | 200 | scan=- drift=- | 08:55:19 |
| S01_NAKAANA1 | 019R | win | 1 | 0.4955 | 3.0 | 1.49 | 200 | scan=- drift=- | 19:04:19 |
| S00 | 241R | win | 1 | 0.4111 | 4.1 | 1.69 | 300 | scan=- drift=- | 17:38:19 |
| S00 | 049R | win | 1 | 0.5123 | 4.5 | 2.31 | 300 | scan=4.8 drift=-6.2% | 16:02:30 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 56 | +22.9% | -73.3% | +533.3% | 15 | 5 | 38 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 341.7s |
| **Latency** (scan→final max) | 601.8s |
| **Traffic** (notifications 24h) | 52 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 399 | 0.4689 | 0.3183 | +0.1506 | 🟡+32% | 0.2355 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 174 | 0.4281 | 0.2874 | 0.2225 | 🔴-0.09 | 0.734 |
| S01_NAKAANA1 | win | 157 | 0.4817 | 0.3057 | 0.2382 | 🔴-0.12 | 0.788 |
| S02_TETSUBAN | win | 68 | 0.5440 | 0.4265 | 0.2626 | 🔴-0.07 | 0.85 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1777 | 0.5714 | 🔴-0.3938 |
| 0.20-0.30 | 16 | 0.2282 | 0.1875 | ✅+0.0407 |
| 0.30-0.50 | 149 | 0.4170 | 0.2819 | 🔴+0.1352 |
| 0.50+ | 220 | 0.5425 | 0.3545 | 🔴+0.1879 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 70 | 0.794 |
| win | <5.0 | ✅learned | 141 | 0.715 |
| win | <10.0 | ✅learned | 73 | 0.471 |
| win | <20.0 | ✅learned | 23 | 0.225 |
| win | <50.0 | ⚠️fallback | 3 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-07-15T12:00:01.873225+09:00_