# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-04T13:40:02.003830+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×21 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 FINAL_MISSING×14 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-04T13:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×33  [2026-06-04T13:06:35]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×40  [2026-06-04T13:04:58]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×39  [2026-06-04T13:04:58]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×35  [2026-06-04T13:04:58]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×5  [2026-06-04T11:50:36]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-06-04T09:00:30]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1957 actual=0.2000 gap=-0.0043`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1265 actual=0.1667 gap=-0.0402`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=7 pred=0.2227 actual=0.4286 gap=-0.2059`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-04T06:00:14]
- key: `ROI_STAT|S00: n=160 hit%=30.0% hit_CI[Bonf]=[20.7,41.2]% ROI=0.90 ROI_boot95=[0.65,1.20]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=160<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-04T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=123 hit%=30.1% hit_CI[Bonf]=[19.7,43.0]% ROI=0.76 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=123<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-04T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=67 hit%=44.8% hit_CI[Bonf]=[28.8,61.9]% ROI=0.81 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=67<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-04T06:00:14]
- key: `ORPHAN_SCAN|216 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-04T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=45 hit%=31.1% ROI=0.88 (コスト 13,100/回収 11,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-04T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=40 hit%=27.5% ROI=0.75 (コスト 8,700/回収 6,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.19MB / last modified 2026-06-04T13:39:06.740032+09:00

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
:38:17,954 [INFO] scraper: odds3t: 120/120 parsed
2026-06-04 13:38:19,082 [INFO] scraper: odds3f: 20/20 parsed
2026-06-04 13:38:20,204 [INFO] scraper: odds2t: 30/30 parsed
2026-06-04 13:38:20,205 [INFO] scraper: odds2f: 14/15 parsed
2026-06-04 13:38:21,296 [INFO] scraper: odds_win: 3/6 parsed
2026-06-04 13:38:21,296 [INFO] scraper: fetch_race 08/8: boats=6 odds=187/191
2026-06-04 13:38:21,299 [INFO] predictor: CALIBRATION_MODE=on
2026-06-04 13:38:21,299 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-06-04 13:38:21,303 [INFO] run_cycle: fetched 08/8 [scan]: 153 combos
2026-06-04 13:38:25,026 [INFO] scraper: odds3t: 120/120 parsed
2026-06-04 13:38:26,176 [INFO] scraper: odds3f: 20/20 parsed
2026-06-04 13:38:27,417 [INFO] scraper: odds2t: 30/30 parsed
2026-06-04 13:38:27,418 [INFO] scraper: odds2f: 15/15 parsed
2026-06-04 13:38:28,570 [INFO] scraper: odds_win: 6/6 parsed
2026-06-04 13:38:28,570 [INFO] scraper: fetch_race 05/5: boats=6 odds=191/191
2026-06-04 13:38:28,573 [INFO] predictor: CALIBRATION_MODE=on
2026-06-04 13:38:28,573 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-04 13:38:28,577 [INFO] run_cycle: fetched 05/5 [scan]: 156 combos
2026-06-04 13:38:28,777 [INFO] race_id: notif: nid=2026060405051351 sid=S01_NAKAANA1 phase=scan rank=B
2026-06-04 13:38:29,320 [INFO] notifier: Discord notify OK (status=204)
2026-06-04 13:38:29,705 [INFO] notifier: Discord notify OK (status=204)
2026-06-04 13:38:29,820 [INFO] run_cycle: SCAN S01_NAKAANA1 多摩川5R B
2026-06-04 13:38:29,927 [INFO] run_cycle: run_cycle done: 1 notifications
2026-06-04 13:39:06,059 [INFO] run_cycle: === run_cycle 13:39:06 ===
2026-06-04 13:39:06,059 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-04 13:39:06,059 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-04 13:39:06,108 [INFO] predictor: Models loaded OK
2026-06-04 13:39:06,398 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 47
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 47
  }
]
```

## Phase別通知記録 (24h)
{'final': 21, 'result': 8, 'scan': 18}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 186
  CIRCUIT_BREAKER_TRIP: 21
  CIRCUIT_BREAKER_NO_ACTION: 18
  STRATEGY_CI_FAIL: 17
  FINAL_MISSING: 14
  ANOMALY_SCAN_FINAL_RATIO: 9
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 6 | 10,800 | 3,390 | -7,410 | 0.314 |
| S01_NAKAANA1 | 41 | 13 | 8,200 | 5,920 | -2,280 | 0.722 |
| S02_TETSUBAN | 20 | 6 | 4,000 | 1,580 | -2,420 | 0.395 |

## 直近アラート (24h・新しい順)
```
[13:39:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1054}
[13:38:29] FINAL_MISSING: {"deadline": "2026-06-04T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060403031208", "sid": "S00"}
[13:38:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1052}
[13:37:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1045}
[13:36:21] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[13:36:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1044}
[13:35:30] CIRCUIT_BREAKER_TRIP: {"cost": 4000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 20, "payout": 1580, "roi_7d": 0.395, "sid": "S02_TETSUBAN"}
[13:35:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1037}
[13:33:17] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 998}
[13:32:16] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1008}
```

## 本日残レース: 85件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 59件 締切済
- 通知発射: scan=11 nid / final=12 nid / result=5 nid
- predictions: 8 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 137R | win | 1 | 0.5476 | 2.0 | 1.10 | 200 | scan=- drift=- | 13:35:29 |
| S01_NAKAANA1 | 1011R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=- drift=- | 13:30:25 |
| S00 | 087R | win | 1 | 0.5476 | 36.7 | 20.10 | 300 | scan=33.7 drift=+8.9% | 13:12:33 |
| S02_TETSUBAN | 096R | win | 1 | 0.5259 | 2.1 | 1.10 | 200 | scan=2.8 drift=-25.0% | 13:02:45 |
| S02_TETSUBAN | 135R | win | 1 | 0.5334 | 2.5 | 1.33 | 200 | scan=2.1 drift=+19.0% | 12:30:32 |
| S00 | 084R | win | 1 | 0.5735 | 7.0 | 4.01 | 300 | scan=- drift=- | 11:49:32 |
| S00 | 032R | win | 1 | 0.1957 | 7.1 | 1.39 | 300 | scan=12.7 drift=-44.1% | 11:38:29 |
| S00 | 093R | win | 1 | 0.4111 | 9.0 | 3.70 | 300 | scan=5.2 drift=+73.1% | 11:28:22 |
| S02_TETSUBAN | 209R | win | 1 | 0.5735 | 2.9 | 1.66 | 200 | scan=- drift=- | 19:06:21 |
| S01_NAKAANA1 | 201R | win | 1 | 0.5990 | 3.0 | 1.80 | 200 | scan=- drift=- | 15:21:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 50 | +17.8% | -81.4% | +432.7% | 14 | 7 | 36 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 462.5s |
| **Latency** (scan→final max) | 660.0s |
| **Traffic** (notifications 24h) | 47 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 346 | 0.4633 | 0.3237 | +0.1396 | 🟡+30% | 0.2378 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 154 | 0.4194 | 0.2922 | 0.2225 | 🔴-0.08 | 0.886 |
| S01_NAKAANA1 | win | 123 | 0.4872 | 0.3008 | 0.2462 | 🔴-0.17 | 0.759 |
| S02_TETSUBAN | win | 69 | 0.5187 | 0.4348 | 0.2571 | 🔴-0.05 | 0.786 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.10-0.15 | 6 | 0.1265 | 0.1667 | ✅-0.0402 |
| 0.15-0.20 | 6 | 0.1957 | 0.1667 | ✅+0.0291 |
| 0.20-0.30 | 6 | 0.2216 | 0.5000 | 🔴-0.2784 |
| 0.30-0.50 | 138 | 0.4186 | 0.2754 | 🔴+0.1432 |
| 0.50+ | 183 | 0.5405 | 0.3770 | 🔴+0.1635 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 30 | 0.748 |
| win | <5.0 | ✅learned | 56 | 0.752 |
| win | <10.0 | ✅learned | 39 | 0.52 |
| win | <20.0 | ✅learned | 12 | 0.197 |
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
_auto-generated by claude_snapshot.py at 2026-06-04T13:40:02.003830+09:00_