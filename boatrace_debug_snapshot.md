# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-14T15:20:02.146504+09:00

### 次に取るべきアクション
> RED最優先: CALIBRATION_DRIFT×36 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×53 (24h)
- 🔴 CALIBRATION_DRIFT×36 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×34 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CALIBRATION_DRIFT  ×1  [2026-09-14T15:19:57]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×16  [2026-09-14T15:04:39]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×48  [2026-09-14T15:04:39]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×16  [2026-09-14T15:04:39]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-14T15:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-14T15:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-14T15:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×22  [2026-09-14T14:58:40]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×11  [2026-09-14T14:26:19]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-14T06:00:57]
- key: `INSUFFICIENT_SAMPLE|S00: n=168<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-14T06:00:57]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1314 actual=0.0000 gap=+0.1314`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-14T06:00:57]
- key: `ROI_STAT|S00: n=168 hit%=27.4% hit_CI[Bonf]=[18.7,38.2]% ROI=0.93 ROI_boot95=[0.63,1.29]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-14T06:00:57]
- key: `ROI_STAT|S01_NAKAANA1: n=182 hit%=24.7% hit_CI[Bonf]=[16.7,34.9]% ROI=0.76 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-14T06:00:57]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=182<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-14T06:00:57]
- key: `ROI_STAT|S02_TETSUBAN: n=85 hit%=34.1% hit_CI[Bonf]=[21.3,49.8]% ROI=0.60 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-14T06:00:57]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=85<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-14T06:00:57]
- key: `ORPHAN_SCAN|176 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-14T06:00:57]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=24.2% ROI=0.69 (コスト 9,500/回収 6,560)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-14T06:00:57]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=27.9% ROI=0.84 (コスト 9,900/回収 8,360)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-14T06:00:57]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=94 hit%=24.5% ROI=0.90 (コスト 21,300/回収 19,230)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.2MB / last modified 2026-09-14T15:19:57.417062+09:00

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
15/15 parsed
2026-09-14 15:19:43,314 [INFO] scraper: odds_win: 6/6 parsed
2026-09-14 15:19:43,315 [INFO] scraper: fetch_race 02/10: boats=6 odds=191/191
2026-09-14 15:19:43,318 [INFO] predictor: CALIBRATION_MODE=on
2026-09-14 15:19:43,318 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-14 15:19:43,322 [INFO] run_cycle: fetched 02/10 [final]: 156 combos
2026-09-14 15:19:46,840 [INFO] scraper: odds3t: 120/120 parsed
2026-09-14 15:19:47,947 [INFO] scraper: odds3f: 20/20 parsed
2026-09-14 15:19:49,028 [INFO] scraper: odds2t: 27/30 parsed
2026-09-14 15:19:49,029 [INFO] scraper: odds2f: 13/15 parsed
2026-09-14 15:19:50,102 [INFO] scraper: odds_win: 2/6 parsed
2026-09-14 15:19:50,102 [INFO] scraper: fetch_race 20/1: boats=6 odds=182/191
2026-09-14 15:19:50,105 [INFO] predictor: CALIBRATION_MODE=on
2026-09-14 15:19:50,105 [INFO] predictor: combos: {'win': 2, '2t': 27, '3t': 120}
2026-09-14 15:19:50,110 [INFO] run_cycle: fetched 20/1 [final]: 149 combos
2026-09-14 15:19:53,837 [INFO] scraper: odds3t: 120/120 parsed
2026-09-14 15:19:54,960 [INFO] scraper: odds3f: 20/20 parsed
2026-09-14 15:19:56,092 [INFO] scraper: odds2t: 30/30 parsed
2026-09-14 15:19:56,093 [INFO] scraper: odds2f: 14/15 parsed
2026-09-14 15:19:57,186 [INFO] scraper: odds_win: 6/6 parsed
2026-09-14 15:19:57,186 [INFO] scraper: fetch_race 04/10: boats=6 odds=190/191
2026-09-14 15:19:57,188 [INFO] predictor: CALIBRATION_MODE=on
2026-09-14 15:19:57,189 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-14 15:19:57,194 [INFO] run_cycle: fetched 04/10 [scan]: 156 combos
2026-09-14 15:19:57,308 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-14 15:20:06,210 [INFO] run_cycle: === run_cycle 15:20:06 ===
2026-09-14 15:20:06,210 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-14 15:20:06,210 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-14 15:20:06,308 [INFO] predictor: Models loaded OK

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
    "c": 75
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 75
  }
]
```

## Phase別通知記録 (24h)
{'final': 26, 'result': 15, 'scan': 34}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 119
  FINAL_MISSING: 53
  CIRCUIT_BREAKER_NO_ACTION: 51
  CALIBRATION_DRIFT: 36
  CIRCUIT_BREAKER_TRIP: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 7
  KS_ODDS_DRIFT: 7
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 28 | 3 | 8,400 | 2,010 | -6,390 | 0.239 |
| S01_NAKAANA1 | 34 | 9 | 6,800 | 5,120 | -1,680 | 0.753 |
| S02_TETSUBAN | 17 | 6 | 3,400 | 1,680 | -1,720 | 0.494 |

## 直近アラート (24h・新しい順)
```
[15:19:57] CALIBRATION_DRIFT: {"avg_actual": 0.2308, "avg_pred": 0.474, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 78, "overconf_pct": 51.3}
[15:19:57] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1155}
[15:18:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1150}
[15:17:35] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1144}
[15:16:47] CIRCUIT_BREAKER_TRIP: {"cost": 8400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 28, "payout": 2010, "roi_7d": 0.239, "sid": "S00"}
[15:16:47] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1131}
[15:14:41] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1122}
[15:13:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1121}
[15:12:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1120}
[15:11:46] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1101}
```

## 本日残レース: 69件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 99件 締切済
- 通知発射: scan=19 nid / final=14 nid / result=7 nid
- predictions: 8 / うち結果DB記録済: 7
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 9件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 071R | win | 1 | 0.5891 | 5.0 | 2.95 | 300 | scan=- drift=- | 15:16:43 |
| S01_NAKAANA1 | 028R | win | 1 | 0.5476 | 4.0 | 2.19 | 200 | scan=- drift=- | 14:13:43 |
| S01_NAKAANA1 | 226R | win | 1 | 0.5123 | 3.9 | 2.00 | 200 | scan=3.5 drift=+11.4% | 14:11:22 |
| S01_NAKAANA1 | 026R | win | 1 | 0.5123 | 3.8 | 1.95 | 200 | scan=4.5 drift=-15.6% | 13:11:20 |
| S01_NAKAANA1 | 024R | win | 1 | 0.5123 | 4.5 | 2.31 | 200 | scan=4.5 drift=+0.0% | 12:11:30 |
| S00 | 094R | win | 1 | 0.2082 | 8.0 | 1.67 | 300 | scan=6.6 drift=+21.2% | 12:00:23 |
| S00 | 042R | win | 1 | 0.5123 | 15.9 | 8.15 | 300 | scan=8.2 drift=+93.9% | 11:21:20 |
| S01_NAKAANA1 | 082R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 11:12:20 |
| S00 | 203R | win | 1 | 0.5735 | 6.0 | 3.44 | 300 | scan=- drift=- | 16:13:21 |
| S02_TETSUBAN | 072R | win | 1 | 0.5476 | 2.2 | 1.20 | 200 | scan=2.0 drift=+10.0% | 15:45:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 47 | +8.0% | -49.1% | +135.7% | 14 | 3 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 465.8s |
| **Latency** (scan→final max) | 626.4s |
| **Traffic** (notifications 24h) | 75 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 430 | 0.4748 | 0.2814 | +0.1934 | 🟡+41% | 0.2409 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 168 | 0.4333 | 0.2738 | 0.2224 | 🔴-0.12 | 0.933 |
| S01_NAKAANA1 | win | 179 | 0.4811 | 0.2570 | 0.2477 | 🔴-0.30 | 0.772 |
| S02_TETSUBAN | win | 83 | 0.5453 | 0.3494 | 0.2638 | 🔴-0.16 | 0.611 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1314 | 0.0000 | 🔴+0.1314 |
| 0.15-0.20 | 6 | 0.1783 | 0.3333 | 🔴-0.1550 |
| 0.20-0.30 | 7 | 0.2214 | 0.0000 | 🔴+0.2214 |
| 0.30-0.50 | 155 | 0.4035 | 0.2323 | 🔴+0.1713 |
| 0.50+ | 253 | 0.5454 | 0.3241 | 🔴+0.2213 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 138 | 0.766 |
| win | <5.0 | ✅learned | 247 | 0.75 |
| win | <10.0 | ✅learned | 121 | 0.468 |
| win | <20.0 | ✅learned | 31 | 0.231 |
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
_auto-generated by claude_snapshot.py at 2026-09-14T15:20:02.146504+09:00_