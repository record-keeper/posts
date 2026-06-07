# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-07T12:40:01.728569+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×72 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×72 (24h)
- 🔴 CALIBRATION_DRIFT×37 (24h)
- 🟡 FINAL_MISSING×30 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×4 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-07T12:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-07T12:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-07T12:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×11  [2026-06-07T12:29:29]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×20  [2026-06-07T12:19:29]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CALIBRATION_DRIFT  ×37  [2026-06-07T12:02:42]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×111  [2026-06-07T12:02:42]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×111  [2026-06-07T12:02:42]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×37  [2026-06-07T12:02:42]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 PSI_DRIFT_DETECTED  ×40  [2026-06-07T11:59:37]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×60  [2026-06-07T09:21:57]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-07T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=5 pred=0.2201 actual=0.4000 gap=-0.1799`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-07T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-07T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1957 actual=0.2000 gap=-0.0043`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-07T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1265 actual=0.1667 gap=-0.0402`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-07T06:00:10]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=36 hit%=25.0% ROI=0.96 (コスト 8,200/回収 7,880)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-07T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=40 hit%=22.5% ROI=0.57 (コスト 8,400/回収 4,750)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-06-07T06:00:10]
- key: `ROI_STAT|S00: n=156 hit%=26.3% hit_CI[Bonf]=[17.5,37.5]% ROI=0.78 ROI_boot95=[0.54,1.06]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-07T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=156<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-07T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=133 hit%=28.6% hit_CI[Bonf]=[18.8,40.9]% ROI=0.71 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.57MB / last modified 2026-06-07T12:39:22.714911+09:00

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
sed
2026-06-07 12:38:21,758 [INFO] scraper: fetch_race 17/5: boats=6 odds=191/191
2026-06-07 12:38:21,770 [INFO] predictor: CALIBRATION_MODE=on
2026-06-07 12:38:21,770 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-07 12:38:21,777 [INFO] run_cycle: fetched 17/5 [scan]: 156 combos
2026-06-07 12:38:25,439 [INFO] scraper: odds3t: 120/120 parsed
2026-06-07 12:38:26,544 [INFO] scraper: odds3f: 20/20 parsed
2026-06-07 12:38:27,657 [INFO] scraper: odds2t: 30/30 parsed
2026-06-07 12:38:27,658 [INFO] scraper: odds2f: 15/15 parsed
2026-06-07 12:38:28,759 [INFO] scraper: odds_win: 5/6 parsed
2026-06-07 12:38:28,759 [INFO] scraper: fetch_race 21/10: boats=6 odds=190/191
2026-06-07 12:38:28,768 [INFO] predictor: CALIBRATION_MODE=on
2026-06-07 12:38:28,768 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-06-07 12:38:28,776 [INFO] run_cycle: fetched 21/10 [scan]: 155 combos
2026-06-07 12:38:28,901 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-07 12:39:06,246 [INFO] run_cycle: === run_cycle 12:39:06 ===
2026-06-07 12:39:06,246 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-07 12:39:06,246 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-07 12:39:06,292 [INFO] predictor: Models loaded OK
2026-06-07 12:39:18,859 [INFO] scraper: odds3t: 120/120 parsed
2026-06-07 12:39:19,998 [INFO] scraper: odds3f: 20/20 parsed
2026-06-07 12:39:21,165 [INFO] scraper: odds2t: 29/30 parsed
2026-06-07 12:39:21,166 [INFO] scraper: odds2f: 14/15 parsed
2026-06-07 12:39:22,263 [INFO] scraper: odds_win: 6/6 parsed
2026-06-07 12:39:22,263 [INFO] scraper: fetch_race 08/6: boats=6 odds=189/191
2026-06-07 12:39:22,275 [INFO] predictor: CALIBRATION_MODE=on
2026-06-07 12:39:22,275 [INFO] predictor: combos: {'win': 6, '2t': 29, '3t': 120}
2026-06-07 12:39:22,283 [INFO] run_cycle: fetched 08/6 [scan]: 155 combos
2026-06-07 12:39:22,473 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 73
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 73
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 18, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 230
  CIRCUIT_BREAKER_TRIP: 72
  CIRCUIT_BREAKER_NO_ACTION: 51
  CALIBRATION_DRIFT: 37
  FINAL_MISSING: 30
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 11
  ANOMALY_BET_VOLUME_SPIKE: 4
  PSI_DRIFT_DETECTED: 4
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 29 | 4 | 8,700 | 2,220 | -6,480 | 0.255 |
| S01_NAKAANA1 | 26 | 2 | 5,200 | 580 | -4,620 | 0.112 |
| S02_TETSUBAN | 26 | 7 | 5,200 | 1,880 | -3,320 | 0.362 |

## 直近アラート (24h・新しい順)
```
[12:38:28] FINAL_MISSING: {"deadline": "2026-06-07T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060703031208", "sid": "S00"}
[12:36:27] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 292, "n_recent": 81, "psi": 0.253}
[12:32:44] CIRCUIT_BREAKER_TRIP: {"cost": 8700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 29, "payout": 2220, "roi_7d": 0.255, "sid": "S00"}
[12:32:44] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 293, "n_recent": 81, "psi": 0.253}
[12:32:44] CALIBRATION_DRIFT: {"avg_actual": 0.1605, "avg_pred": 0.4852, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 81, "overconf_pct": 66.9}
[12:30:36] CIRCUIT_BREAKER_TRIP: {"cost": 9000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 30, "payout": 2220, "roi_7d": 0.247, "sid": "S00"}
[12:30:36] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 292, "n_recent": 82, "psi": 0.253}
[12:30:36] CALIBRATION_DRIFT: {"avg_actual": 0.1585, "avg_pred": 0.4853, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 82, "overconf_pct": 67.3}
[12:30:36] FINAL_MISSING: {"deadline": "2026-06-07T11:00:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060718061100", "sid": "S00"}
[12:29:29] CIRCUIT_BREAKER_TRIP: {"cost": 5200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 26, "payout": 580, "roi_7d": 0.112, "sid": "S01_NAKAANA1"}
```

## 本日残レース: 105件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 51件 締切済
- 通知発射: scan=9 nid / final=11 nid / result=8 nid
- predictions: 9 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 188R | win | 1 | 0.1231 | 4.4 | 0.54 | 300 | scan=- drift=- | 11:59:21 |
| S02_TETSUBAN | 032R | win | 1 | 0.5334 | 2.3 | 1.23 | 200 | scan=- drift=- | 11:39:20 |
| S01_NAKAANA1 | 187R | win | 1 | 0.5123 | 4.5 | 2.31 | 200 | scan=4.3 drift=+4.7% | 11:28:22 |
| S00 | 187R | win | 1 | 0.5123 | 4.5 | 2.31 | 300 | scan=4.3 drift=+4.7% | 11:28:21 |
| S01_NAKAANA1 | 217R | win | 1 | 0.5891 | 4.5 | 2.65 | 200 | scan=- drift=- | 11:15:32 |
| S01_NAKAANA1 | 031R | win | 1 | 0.5123 | 3.6 | 1.84 | 200 | scan=- drift=- | 11:11:21 |
| S01_NAKAANA1 | 186R | win | 1 | 0.5174 | 4.7 | 2.43 | 200 | scan=4.7 drift=+0.0% | 10:57:20 |
| S00 | 082R | win | 1 | 0.5891 | 25.1 | 14.79 | 300 | scan=6.7 drift=+274.6% | 10:55:22 |
| S02_TETSUBAN | 213R | win | 1 | 0.5476 | 2.1 | 1.15 | 200 | scan=- drift=- | 09:22:21 |
| S02_TETSUBAN | 0712R | win | 1 | 0.5735 | 2.6 | 1.49 | 200 | scan=- drift=- | 20:43:45 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 42 | +13.9% | -62.9% | +432.7% | 16 | 8 | 29 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 450.2s |
| **Latency** (scan→final max) | 600.4s |
| **Traffic** (notifications 24h) | 73 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 373 | 0.4662 | 0.2922 | +0.1740 | 🟡+37% | 0.2375 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 157 | 0.4210 | 0.2484 | 0.2201 | 🔴-0.18 | 0.745 |
| S01_NAKAANA1 | win | 137 | 0.4850 | 0.2774 | 0.2436 | 🔴-0.22 | 0.693 |
| S02_TETSUBAN | win | 79 | 0.5235 | 0.4051 | 0.2615 | 🔴-0.08 | 0.722 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.10-0.15 | 7 | 0.1260 | 0.1429 | ✅-0.0169 |
| 0.15-0.20 | 5 | 0.1957 | 0.2000 | ✅-0.0043 |
| 0.20-0.30 | 5 | 0.2201 | 0.4000 | 🔴-0.1799 |
| 0.30-0.50 | 150 | 0.4185 | 0.2400 | 🔴+0.1785 |
| 0.50+ | 199 | 0.5416 | 0.3467 | 🔴+0.1949 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 32 | 0.741 |
| win | <5.0 | ✅learned | 59 | 0.732 |
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
_auto-generated by claude_snapshot.py at 2026-06-07T12:40:01.728569+09:00_