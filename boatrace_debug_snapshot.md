# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-26T12:50:01.325051+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×41 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×72 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×41 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×60  [2026-09-26T12:03:12]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×92  [2026-09-26T12:03:12]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×46  [2026-09-26T12:03:12]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-26T12:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-26T12:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×34  [2026-09-26T11:51:40]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×15  [2026-09-26T11:13:38]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-26T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-26T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S00: n=169<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-26T06:00:21]
- key: `ORPHAN_SCAN|162 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-26T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=154<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-26T06:00:21]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0760 actual=0.2000 gap=-0.1240`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-26T06:00:21]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=31 pred=0.3235 actual=0.2258 gap=+0.0977`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-26T06:00:21]
- key: `ROI_STAT|S00: n=169 hit%=22.5% hit_CI[Bonf]=[14.6,32.9]% ROI=0.69 ROI_boot95=[0.46,0.96]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-26T06:00:21]
- key: `ROI_STAT|S01_NAKAANA1: n=154 hit%=22.7% hit_CI[Bonf]=[14.5,33.7]% ROI=0.68 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-26T06:00:21]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=45.0% hit_CI[Bonf]=[30.2,60.8]% ROI=0.83 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-26T06:00:21]
- key: `DRIFT_BUCKET|drift ≤-30%: n=30 hit%=30.0% ROI=0.92 (コスト 8,500/回収 7,850)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-26T06:00:21]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=39 hit%=25.6% ROI=0.71 (コスト 8,800/回収 6,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-26T06:00:21]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=89 hit%=23.6% ROI=0.71 (コスト 20,600/回収 14,620)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-26T06:00:21]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=40 hit%=27.5% ROI=0.52 (コスト 9,000/回収 4,680)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 14.18MB / last modified 2026-09-26T12:49:39.854137+09:00

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
 combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-26 12:49:18,892 [INFO] run_cycle: fetched 09/6 [scan]: 156 combos
2026-09-26 12:49:22,432 [INFO] scraper: odds3t: 120/120 parsed
2026-09-26 12:49:23,532 [INFO] scraper: odds3f: 20/20 parsed
2026-09-26 12:49:24,616 [INFO] scraper: odds2t: 30/30 parsed
2026-09-26 12:49:24,617 [INFO] scraper: odds2f: 15/15 parsed
2026-09-26 12:49:25,733 [INFO] scraper: odds_win: 5/6 parsed
2026-09-26 12:49:25,734 [INFO] scraper: fetch_race 08/6: boats=6 odds=190/191
2026-09-26 12:49:25,736 [INFO] predictor: CALIBRATION_MODE=on
2026-09-26 12:49:25,736 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-09-26 12:49:25,740 [INFO] run_cycle: fetched 08/6 [scan]: 155 combos
2026-09-26 12:49:29,211 [INFO] scraper: odds3t: 120/120 parsed
2026-09-26 12:49:30,346 [INFO] scraper: odds3f: 20/20 parsed
2026-09-26 12:49:31,540 [INFO] scraper: odds2t: 30/30 parsed
2026-09-26 12:49:31,541 [INFO] scraper: odds2f: 14/15 parsed
2026-09-26 12:49:32,646 [INFO] scraper: odds_win: 6/6 parsed
2026-09-26 12:49:32,646 [INFO] scraper: fetch_race 18/10: boats=6 odds=190/191
2026-09-26 12:49:32,649 [INFO] predictor: CALIBRATION_MODE=on
2026-09-26 12:49:32,649 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-26 12:49:32,653 [INFO] run_cycle: fetched 18/10 [scan]: 156 combos
2026-09-26 12:49:36,260 [INFO] scraper: odds3t: 120/120 parsed
2026-09-26 12:49:37,382 [INFO] scraper: odds3f: 20/20 parsed
2026-09-26 12:49:38,519 [INFO] scraper: odds2t: 29/30 parsed
2026-09-26 12:49:38,520 [INFO] scraper: odds2f: 12/15 parsed
2026-09-26 12:49:39,593 [INFO] scraper: odds_win: 3/6 parsed
2026-09-26 12:49:39,593 [INFO] scraper: fetch_race 03/5: boats=6 odds=184/191
2026-09-26 12:49:39,595 [INFO] predictor: CALIBRATION_MODE=on
2026-09-26 12:49:39,596 [INFO] predictor: combos: {'win': 3, '2t': 29, '3t': 120}
2026-09-26 12:49:39,599 [INFO] run_cycle: fetched 03/5 [scan]: 152 combos
2026-09-26 12:49:39,746 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 89
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 89
  }
]
```

## Phase別通知記録 (24h)
{'final': 35, 'result': 19, 'scan': 35}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 137
  FINAL_MISSING: 72
  CIRCUIT_BREAKER_TRIP: 41
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_BET_VOLUME_SPIKE: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 6
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 7 | 10,800 | 4,890 | -5,910 | 0.453 |
| S01_NAKAANA1 | 35 | 10 | 7,000 | 5,080 | -1,920 | 0.726 |
| S02_TETSUBAN | 22 | 12 | 4,400 | 4,700 | +300 | 1.068 |

## 直近アラート (24h・新しい順)
```
[12:49:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1246}
[12:48:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1247}
[12:47:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1264}
[12:46:46] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1258}
[12:45:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1237}
[12:44:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1257}
[12:43:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1265}
[12:41:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1261}
[12:40:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1266}
[12:39:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1257}
```

## 本日残レース: 101件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 55件 締切済
- 通知発射: scan=16 nid / final=14 nid / result=6 nid
- predictions: 7 / うち結果DB記録済: 6
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 054R | win | 1 | 0.3229 | 19.2 | 6.20 | 300 | scan=4.2 drift=+357.1% | 12:30:23 |
| S01_NAKAANA1 | 024R | win | 1 | 0.5891 | 3.5 | 2.06 | 200 | scan=4.8 drift=-27.1% | 12:11:20 |
| S01_NAKAANA1 | 218R | win | 1 | 0.4989 | 3.7 | 1.85 | 200 | scan=3.7 drift=+0.0% | 12:04:19 |
| S01_NAKAANA1 | 114R | win | 1 | 0.5735 | 3.7 | 2.12 | 200 | scan=3.0 drift=+23.3% | 11:46:30 |
| S00 | 083R | win | 1 | 0.5334 | 4.1 | 2.19 | 300 | scan=10.5 drift=-61.0% | 11:30:22 |
| S01_NAKAANA1 | 092R | win | 1 | 0.5891 | 3.7 | 2.18 | 200 | scan=- drift=- | 10:59:30 |
| S02_TETSUBAN | 213R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=2.6 drift=-15.4% | 09:33:21 |
| S01_NAKAANA1 | 196R | win | 1 | 0.5735 | 3.0 | 1.72 | 200 | scan=- drift=- | 17:32:33 |
| S02_TETSUBAN | 204R | win | 1 | 0.4989 | 2.1 | 1.05 | 200 | scan=- drift=- | 16:22:20 |
| S00 | 192R | win | 1 | 0.4111 | 4.3 | 1.77 | 300 | scan=- drift=- | 15:40:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 58 | +4.0% | -72.2% | +357.1% | 21 | 7 | 37 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 485.5s |
| **Latency** (scan→final max) | 671.0s |
| **Traffic** (notifications 24h) | 89 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 403 | 0.4783 | 0.2705 | +0.2079 | 🟡+44% | 0.2463 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 168 | 0.4453 | 0.2262 | 0.2356 | 🔴-0.35 | 0.696 |
| S01_NAKAANA1 | win | 154 | 0.4891 | 0.2273 | 0.2507 | 🔴-0.43 | 0.668 |
| S02_TETSUBAN | win | 81 | 0.5265 | 0.4444 | 0.2600 | 🔴-0.05 | 0.825 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 153 | 0.4153 | 0.2418 | 🔴+0.1735 |
| 0.50+ | 233 | 0.5449 | 0.2961 | 🔴+0.2488 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 156 | 0.782 |
| win | <5.0 | ✅learned | 270 | 0.755 |
| win | <10.0 | ✅learned | 126 | 0.46 |
| win | <20.0 | ✅learned | 34 | 0.237 |
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
_auto-generated by claude_snapshot.py at 2026-09-26T12:50:01.325051+09:00_