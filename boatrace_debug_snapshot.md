# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-22T15:20:01.559032+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×28 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×44 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×28 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×32  [2026-06-22T15:04:30]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×32  [2026-06-22T15:04:30]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×16  [2026-06-22T15:04:30]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-06-22T15:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-22T15:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-22T15:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×37  [2026-06-22T14:42:18]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×20  [2026-06-22T12:58:39]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×41  [2026-06-22T10:00:26]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-22T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=141<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-22T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=149<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-22T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-22T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2241 actual=0.1111 gap=+0.1130`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-22T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0816 actual=0.0000 gap=+0.0816`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-22T06:00:12]
- key: `ROI_STAT|S00: n=149 hit%=26.2% hit_CI[Bonf]=[17.2,37.6]% ROI=0.71 ROI_boot95=[0.51,0.95]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-22T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=141 hit%=27.7% hit_CI[Bonf]=[18.3,39.5]% ROI=0.73 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-22T06:00:12]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=35.0% hit_CI[Bonf]=[21.7,51.1]% ROI=0.59 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-22T06:00:12]
- key: `ORPHAN_SCAN|156 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-22T06:00:12]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=20.6% ROI=0.67 (コスト 9,700/回収 6,510)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-22T06:00:12]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=20.0% ROI=0.44 (コスト 8,000/回収 3,510)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.7MB / last modified 2026-06-22T15:19:54.762711+09:00

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
mbos: {'win': 6, '2t': 30, '3t': 120}
2026-06-22 15:19:22,659 [INFO] run_cycle: fetched 02/10 [final]: 156 combos
2026-06-22 15:19:26,221 [INFO] scraper: odds3t: 120/120 parsed
2026-06-22 15:19:27,333 [INFO] scraper: odds3f: 20/20 parsed
2026-06-22 15:19:28,439 [INFO] scraper: odds2t: 30/30 parsed
2026-06-22 15:19:28,441 [INFO] scraper: odds2f: 15/15 parsed
2026-06-22 15:19:29,550 [INFO] scraper: odds_win: 6/6 parsed
2026-06-22 15:19:29,550 [INFO] scraper: fetch_race 24/1: boats=6 odds=191/191
2026-06-22 15:19:29,559 [INFO] predictor: CALIBRATION_MODE=on
2026-06-22 15:19:29,559 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-22 15:19:29,568 [INFO] run_cycle: fetched 24/1 [final]: 156 combos
2026-06-22 15:19:33,362 [INFO] scraper: odds3t: 120/120 parsed
2026-06-22 15:19:34,484 [INFO] scraper: odds3f: 19/20 parsed
2026-06-22 15:19:35,617 [INFO] scraper: odds2t: 29/30 parsed
2026-06-22 15:19:35,618 [INFO] scraper: odds2f: 15/15 parsed
2026-06-22 15:19:36,741 [INFO] scraper: odds_win: 2/6 parsed
2026-06-22 15:19:36,741 [INFO] scraper: fetch_race 19/1: boats=6 odds=185/191
2026-06-22 15:19:36,751 [INFO] predictor: CALIBRATION_MODE=on
2026-06-22 15:19:36,753 [INFO] predictor: combos: {'win': 2, '2t': 29, '3t': 120}
2026-06-22 15:19:36,762 [INFO] run_cycle: fetched 19/1 [scan]: 151 combos
2026-06-22 15:19:40,720 [INFO] scraper: odds3t: 120/120 parsed
2026-06-22 15:19:41,968 [INFO] scraper: odds3f: 20/20 parsed
2026-06-22 15:19:43,128 [INFO] scraper: odds2t: 30/30 parsed
2026-06-22 15:19:43,129 [INFO] scraper: odds2f: 15/15 parsed
2026-06-22 15:19:44,399 [INFO] scraper: odds_win: 6/6 parsed
2026-06-22 15:19:44,401 [INFO] scraper: fetch_race 17/10: boats=6 odds=191/191
2026-06-22 15:19:44,416 [INFO] predictor: CALIBRATION_MODE=on
2026-06-22 15:19:44,416 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-22 15:19:44,425 [INFO] run_cycle: fetched 17/10 [scan]: 156 combos
2026-06-22 15:19:44,526 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 50
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 50
  }
]
```

## Phase別通知記録 (24h)
{'final': 18, 'result': 13, 'scan': 19}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 129
  FINAL_MISSING: 44
  CIRCUIT_BREAKER_NO_ACTION: 36
  CIRCUIT_BREAKER_TRIP: 28
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 2
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 39 | 10 | 11,700 | 8,010 | -3,690 | 0.685 |
| S01_NAKAANA1 | 36 | 7 | 7,200 | 3,100 | -4,100 | 0.431 |
| S02_TETSUBAN | 14 | 5 | 2,800 | 1,920 | -880 | 0.686 |

## 直近アラート (24h・新しい順)
```
[15:19:44] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1138}
[15:17:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1117}
[15:16:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1112}
[15:15:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1111}
[15:14:42] FINAL_MISSING: {"deadline": "2026-06-22T14:44:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062211091444", "sid": "S02_TETSUBAN"}
[15:13:40] FINAL_MISSING: {"deadline": "2026-06-22T13:43:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062216061343", "sid": "S00"}
[15:12:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1100}
[15:11:49] CIRCUIT_BREAKER_TRIP: {"cost": 11700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 39, "payout": 8010, "roi_7d": 0.685, "sid": "S00"}
[15:11:49] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1090}
[15:10:10] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1085}
```

## 本日残レース: 64件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 104件 締切済
- 通知発射: scan=11 nid / final=10 nid / result=6 nid
- predictions: 7 / うち結果DB記録済: 7
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 167R | win | 1 | 0.5174 | 12.5 | 6.47 | 300 | scan=6.0 drift=+108.3% | 14:11:25 |
| S01_NAKAANA1 | 055R | win | 1 | 0.3177 | 4.3 | 1.37 | 200 | scan=- drift=- | 13:30:32 |
| S00 | 055R | win | 1 | 0.3177 | 4.3 | 1.37 | 300 | scan=- drift=- | 13:30:29 |
| S00 | 1011R | win | 1 | 0.5174 | 7.6 | 3.93 | 300 | scan=6.3 drift=+20.6% | 13:21:22 |
| S00 | 222R | win | 1 | 0.3177 | 26.2 | 8.32 | 300 | scan=4.5 drift=+482.2% | 12:58:23 |
| S01_NAKAANA1 | 084R | win | 1 | 0.4111 | 4.1 | 1.69 | 200 | scan=- drift=- | 11:54:20 |
| S01_NAKAANA1 | 106R | win | 1 | 0.5714 | 3.7 | 2.11 | 200 | scan=3.5 drift=+5.7% | 10:41:22 |
| S01_NAKAANA1 | 203R | win | 1 | 0.4989 | 3.8 | 1.90 | 200 | scan=3.0 drift=+26.7% | 18:31:21 |
| S00 | 194R | win | 1 | 0.5891 | 21.7 | 12.78 | 300 | scan=20.2 drift=+7.4% | 16:54:22 |
| S00 | 154R | win | 1 | 0.5174 | 6.6 | 3.41 | 300 | scan=7.5 drift=-12.0% | 16:42:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 52 | +7.4% | -61.4% | +482.2% | 18 | 8 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 473.2s |
| **Latency** (scan→final max) | 605.7s |
| **Traffic** (notifications 24h) | 50 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 370 | 0.4733 | 0.2811 | +0.1922 | 🟡+41% | 0.2415 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 151 | 0.4255 | 0.2517 | 0.2236 | 🔴-0.19 | 0.679 |
| S01_NAKAANA1 | win | 142 | 0.4890 | 0.2746 | 0.2452 | 🔴-0.23 | 0.727 |
| S02_TETSUBAN | win | 77 | 0.5380 | 0.3506 | 0.2699 | 🔴-0.19 | 0.587 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0816 | 0.0000 | 🔴+0.0816 |
| 0.15-0.20 | 7 | 0.1808 | 0.4286 | 🔴-0.2478 |
| 0.20-0.30 | 9 | 0.2241 | 0.1111 | 🔴+0.1130 |
| 0.30-0.50 | 126 | 0.4228 | 0.2381 | 🔴+0.1847 |
| 0.50+ | 217 | 0.5423 | 0.3180 | 🔴+0.2243 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 46 | 0.733 |
| win | <5.0 | ✅learned | 88 | 0.737 |
| win | <10.0 | ✅learned | 56 | 0.499 |
| win | <20.0 | ✅learned | 15 | 0.207 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-06-22T15:20:01.559032+09:00_