# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-21T15:30:01.946524+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×19 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×68 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×19 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×24  [2026-06-21T15:06:30]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-21T15:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-21T15:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×90  [2026-06-21T14:45:44]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 CIRCUIT_BREAKER_TRIP  ×82  [2026-06-21T14:43:47]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×27  [2026-06-21T13:30:26]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×5  [2026-06-21T11:47:33]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×9  [2026-06-21T11:00:33]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-21T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=141<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-21T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=146<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-21T06:00:10]
- key: `DRIFT_BUCKET|drift ≥+30%: n=26 hit%=23.1% ROI=0.48 (コスト 7,200/回収 3,450)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-21T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2246 actual=0.1000 gap=+0.1246`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-21T06:00:10]
- key: `ROI_STAT|S00: n=146 hit%=26.7% hit_CI[Bonf]=[17.6,38.3]% ROI=0.76 ROI_boot95=[0.53,1.03]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-21T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=141 hit%=28.4% hit_CI[Bonf]=[18.9,40.3]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-21T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=81 hit%=37.0% hit_CI[Bonf]=[23.4,53.0]% ROI=0.63 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-21T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-21T06:00:10]
- key: `ORPHAN_SCAN|154 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-21T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=36 hit%=22.2% ROI=0.66 (コスト 10,300/回収 6,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-21T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=33 hit%=15.2% ROI=0.24 (コスト 7,300/回収 1,740)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-21T06:00:10]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=72 hit%=31.9% ROI=0.76 (コスト 16,900/回収 12,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.66MB / last modified 2026-06-21T15:30:04.703342+09:00

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
2026-06-21 15:28:32,373 [INFO] scraper: fetch_race 17/10: boats=6 odds=190/191
2026-06-21 15:28:32,384 [INFO] predictor: CALIBRATION_MODE=on
2026-06-21 15:28:32,384 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-06-21 15:28:32,395 [INFO] run_cycle: fetched 17/10 [final]: 155 combos
2026-06-21 15:28:35,972 [INFO] scraper: odds3t: 120/120 parsed
2026-06-21 15:28:37,081 [INFO] scraper: odds3f: 20/20 parsed
2026-06-21 15:28:38,199 [INFO] scraper: odds2t: 30/30 parsed
2026-06-21 15:28:38,201 [INFO] scraper: odds2f: 14/15 parsed
2026-06-21 15:28:39,287 [INFO] scraper: odds_win: 3/6 parsed
2026-06-21 15:28:39,287 [INFO] scraper: fetch_race 08/11: boats=6 odds=187/191
2026-06-21 15:28:39,298 [INFO] predictor: CALIBRATION_MODE=on
2026-06-21 15:28:39,298 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-06-21 15:28:39,305 [INFO] run_cycle: fetched 08/11 [scan]: 153 combos
2026-06-21 15:28:39,562 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-21 15:29:05,954 [INFO] run_cycle: === run_cycle 15:29:05 ===
2026-06-21 15:29:05,954 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-21 15:29:05,954 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-21 15:29:05,999 [INFO] predictor: Models loaded OK
2026-06-21 15:29:18,470 [INFO] scraper: odds3t: 120/120 parsed
2026-06-21 15:29:19,622 [INFO] scraper: odds3f: 20/20 parsed
2026-06-21 15:29:20,768 [INFO] scraper: odds2t: 30/30 parsed
2026-06-21 15:29:20,769 [INFO] scraper: odds2f: 15/15 parsed
2026-06-21 15:29:21,938 [INFO] scraper: odds_win: 6/6 parsed
2026-06-21 15:29:21,939 [INFO] scraper: fetch_race 04/8: boats=6 odds=191/191
2026-06-21 15:29:21,950 [INFO] predictor: CALIBRATION_MODE=on
2026-06-21 15:29:21,950 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-21 15:29:21,958 [INFO] run_cycle: fetched 04/8 [final]: 156 combos
2026-06-21 15:29:22,332 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 67
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 67
  }
]
```

## Phase別通知記録 (24h)
{'final': 26, 'result': 18, 'scan': 23}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 74
  FINAL_MISSING: 68
  CIRCUIT_BREAKER_TRIP: 19
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 10
  CIRCUIT_BREAKER_NO_ACTION: 9
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 10 | 10,500 | 7,260 | -3,240 | 0.691 |
| S01_NAKAANA1 | 35 | 7 | 7,000 | 3,100 | -3,900 | 0.443 |
| S02_TETSUBAN | 14 | 5 | 2,800 | 1,920 | -880 | 0.686 |

## 直近アラート (24h・新しい順)
```
[15:26:06] CIRCUIT_BREAKER_TRIP: {"cost": 10500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 7260, "roi_7d": 0.691, "sid": "S00"}
[15:26:06] FINAL_MISSING: {"deadline": "2026-06-21T14:56:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062117091456", "sid": "S00"}
[15:24:36] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[15:06:30] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[14:55:31] CIRCUIT_BREAKER_TRIP: {"cost": 7000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 3100, "roi_7d": 0.443, "sid": "S01_NAKAANA1"}
[14:48:06] FINAL_MISSING: {"deadline": "2026-06-21T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062102021116", "sid": "S00"}
[14:45:43] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[14:33:45] CIRCUIT_BREAKER_TRIP: {"cost": 6800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 3100, "roi_7d": 0.456, "sid": "S01_NAKAANA1"}
[14:25:43] CIRCUIT_BREAKER_TRIP: {"cost": 10500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 7260, "roi_7d": 0.691, "sid": "S00"}
[14:23:21] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
```

## 本日残レース: 72件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 192件 登録 / 120件 締切済
- 通知発射: scan=15 nid / final=17 nid / result=13 nid
- predictions: 15 / うち結果DB記録済: 15
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 0810R | win | 1 | 0.4111 | 4.5 | 1.85 | 200 | scan=4.5 drift=+0.0% | 14:55:23 |
| S00 | 0810R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=4.5 drift=+0.0% | 14:55:22 |
| S00 | 045R | win | 1 | 0.1760 | 4.1 | 0.72 | 300 | scan=5.5 drift=-25.5% | 13:52:22 |
| S02_TETSUBAN | 167R | win | 1 | 0.5719 | 2.6 | 1.49 | 200 | scan=2.0 drift=+30.0% | 13:39:26 |
| S00 | 087R | win | 1 | 0.4989 | 5.0 | 2.49 | 300 | scan=6.3 drift=-20.6% | 13:28:21 |
| S00 | 176R | win | 1 | 0.5083 | 5.6 | 2.85 | 300 | scan=5.2 drift=+7.7% | 13:20:23 |
| S01_NAKAANA1 | 026R | win | 1 | 0.5493 | 4.8 | 2.64 | 200 | scan=- drift=- | 13:11:21 |
| S01_NAKAANA1 | 054R | win | 1 | 0.5123 | 4.8 | 2.46 | 200 | scan=- drift=- | 13:00:38 |
| S00 | 054R | win | 1 | 0.5123 | 4.8 | 2.46 | 300 | scan=7.5 drift=-36.0% | 13:00:28 |
| S00 | 042R | win | 1 | 0.3177 | 7.5 | 2.38 | 300 | scan=- drift=- | 12:21:38 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 49 | -6.5% | -61.4% | +43.3% | 20 | 9 | 30 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 381.3s |
| **Latency** (scan→final max) | 599.4s |
| **Traffic** (notifications 24h) | 67 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,100円 used |
| **Saturation** (S01_NAKAANA1) | 1,200円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 372 | 0.4733 | 0.2876 | +0.1857 | 🟡+39% | 0.2427 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 147 | 0.4226 | 0.2653 | 0.2257 | 🔴-0.16 | 0.712 |
| S01_NAKAANA1 | win | 145 | 0.4896 | 0.2759 | 0.2456 | 🔴-0.23 | 0.723 |
| S02_TETSUBAN | win | 80 | 0.5368 | 0.3500 | 0.2687 | 🔴-0.18 | 0.593 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0816 | 0.0000 | 🔴+0.0816 |
| 0.15-0.20 | 7 | 0.1808 | 0.4286 | 🔴-0.2478 |
| 0.20-0.30 | 9 | 0.2241 | 0.1111 | 🔴+0.1130 |
| 0.30-0.50 | 128 | 0.4234 | 0.2500 | 🔴+0.1734 |
| 0.50+ | 217 | 0.5424 | 0.3226 | 🔴+0.2199 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 46 | 0.733 |
| win | <5.0 | ✅learned | 88 | 0.737 |
| win | <10.0 | ✅learned | 55 | 0.495 |
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
_auto-generated by claude_snapshot.py at 2026-06-21T15:30:01.946524+09:00_