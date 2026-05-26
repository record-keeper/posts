# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-26T18:50:01.955600+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×71 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×15 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×7 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-05-26T18:49:29]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 CIRCUIT_BREAKER_TRIP  ×2  [2026-05-26T18:48:06]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 PSI_DRIFT_DETECTED  ×21  [2026-05-26T18:29:21]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×43  [2026-05-26T18:07:05]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-05-26T18:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_DROP  ×47  [2026-05-26T15:00:40]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 KS_ODDS_DRIFT  ×10  [2026-05-26T13:36:22]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×14  [2026-05-26T12:10:49]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×16  [2026-05-26T11:49:57]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-05-26T11:20:26]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-05-26T10:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-26T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=183<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-26T06:00:11]
- key: `ORPHAN_SCAN|234 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-26T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=12 pred=0.2243 actual=0.3333 gap=-0.1090`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-26T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=26 pred=0.3234 actual=0.2308 gap=+0.0926`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-26T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=49 hit%=32.7% ROI=0.88 (コスト 14,500/回収 12,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-05-26T06:00:11]
- key: `ROI_STAT|S00: n=183 hit%=27.3% hit_CI[Bonf]=[19.0,37.7]% ROI=0.91 ROI_boot95=[0.66,1.19]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-26T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=81 hit%=27.2% hit_CI[Bonf]=[15.5,43.0]% ROI=0.71 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-26T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-26T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=45 hit%=46.7% hit_CI[Bonf]=[27.5,66.9]% ROI=0.86 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.56MB / last modified 2026-05-26T18:49:29.885018+09:00

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
== run_cycle 18:48:05 ===
2026-05-26 18:48:05,979 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-26 18:48:05,979 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-26 18:48:06,050 [INFO] predictor: Models loaded OK
2026-05-26 18:48:06,153 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-26 18:49:05,992 [INFO] run_cycle: === run_cycle 18:49:05 ===
2026-05-26 18:49:05,992 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-26 18:49:05,992 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-26 18:49:06,034 [INFO] predictor: Models loaded OK
2026-05-26 18:49:18,952 [INFO] scraper: odds3t: 120/120 parsed
2026-05-26 18:49:20,042 [INFO] scraper: odds3f: 20/20 parsed
2026-05-26 18:49:21,146 [INFO] scraper: odds2t: 30/30 parsed
2026-05-26 18:49:21,147 [INFO] scraper: odds2f: 15/15 parsed
2026-05-26 18:49:22,259 [INFO] scraper: odds_win: 5/6 parsed
2026-05-26 18:49:22,259 [INFO] scraper: fetch_race 12/8: boats=6 odds=190/191
2026-05-26 18:49:22,272 [INFO] predictor: CALIBRATION_MODE=on
2026-05-26 18:49:22,272 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-05-26 18:49:22,280 [INFO] run_cycle: fetched 12/8 [final]: 155 combos
2026-05-26 18:49:26,273 [INFO] scraper: odds3t: 120/120 parsed
2026-05-26 18:49:27,394 [INFO] scraper: odds3f: 20/20 parsed
2026-05-26 18:49:28,519 [INFO] scraper: odds2t: 30/30 parsed
2026-05-26 18:49:28,520 [INFO] scraper: odds2f: 15/15 parsed
2026-05-26 18:49:29,656 [INFO] scraper: odds_win: 2/6 parsed
2026-05-26 18:49:29,656 [INFO] scraper: fetch_race 07/8: boats=6 odds=187/191
2026-05-26 18:49:29,665 [INFO] predictor: CALIBRATION_MODE=on
2026-05-26 18:49:29,665 [INFO] predictor: combos: {'win': 2, '2t': 30, '3t': 120}
2026-05-26 18:49:29,673 [INFO] run_cycle: fetched 07/8 [scan]: 152 combos
2026-05-26 18:49:29,789 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 48
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 48
  }
]
```

## Phase別通知記録 (24h)
{'final': 21, 'result': 8, 'scan': 19}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 71
  ANOMALY_SCRAPER_FAILURE_BURST: 51
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 15
  ANOMALY_SCAN_FINAL_RATIO: 14
  KS_ODDS_DRIFT: 12
  CIRCUIT_BREAKER_TRIP: 7
  CIRCUIT_BREAKER_NO_ACTION: 6
  ANOMALY_BET_VOLUME_DROP: 4
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 11 | 10,800 | 10,620 | -180 | 0.983 |
| S01_NAKAANA1 | 32 | 8 | 6,400 | 4,020 | -2,380 | 0.628 |
| S02_TETSUBAN | 14 | 7 | 2,800 | 2,320 | -480 | 0.829 |

## 直近アラート (24h・新しい順)
```
[18:49:29] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[18:42:06] FINAL_MISSING: {"deadline": "2026-05-26T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052603031208", "sid": "S00"}
[18:26:28] FINAL_MISSING: {"deadline": "2026-05-26T12:54:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052610101254", "sid": "S00"}
[18:24:23] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 228, "n_recent": 82, "psi": 0.544}
[18:11:27] CIRCUIT_BREAKER_TRIP: {"cost": 6400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 32, "payout": 4020, "roi_7d": 0.628, "sid": "S01_NAKAANA1"}
[18:06:21] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[17:55:31] FINAL_MISSING: {"deadline": "2026-05-26T11:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052610071122", "sid": "S00"}
[17:49:17] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[17:41:21] FINAL_MISSING: {"deadline": "2026-05-26T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052603031208", "sid": "S00"}
[17:39:47] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 228, "n_recent": 81, "psi": 0.575}
```

## 本日残レース: 18件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 114件 締切済
- 通知発射: scan=17 nid / final=18 nid / result=7 nid
- predictions: 8 / うち結果DB記録済: 7
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 127R | win | 1 | 0.2173 | 9.8 | 2.13 | 300 | scan=- drift=- | 18:24:21 |
| S01_NAKAANA1 | 123R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=4.1 drift=-24.4% | 16:39:32 |
| S00 | 152R | win | 1 | 0.4111 | 11.2 | 4.60 | 300 | scan=7.5 drift=+49.3% | 15:47:21 |
| S01_NAKAANA1 | 1010R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=- drift=- | 12:51:22 |
| S00 | 109R | win | 1 | 0.3177 | 12.9 | 4.10 | 300 | scan=19.1 drift=-32.5% | 12:19:32 |
| S00 | 174R | win | 1 | 0.4111 | 5.7 | 2.34 | 300 | scan=15.0 drift=-62.0% | 12:12:46 |
| S02_TETSUBAN | 032R | win | 1 | 0.5174 | 2.4 | 1.24 | 200 | scan=- drift=- | 11:39:20 |
| S00 | 106R | win | 1 | 0.5123 | 5.0 | 2.56 | 300 | scan=- drift=- | 10:47:22 |
| S01_NAKAANA1 | 1210R | win | 1 | 0.5735 | 3.5 | 2.01 | 200 | scan=- drift=- | 19:39:21 |
| S00 | 126R | win | 1 | 0.5123 | 5.6 | 2.87 | 300 | scan=- drift=- | 17:56:33 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 51 | -2.5% | -78.6% | +157.5% | 21 | 12 | 38 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 563.5s |
| **Latency** (scan→final max) | 672.5s |
| **Traffic** (notifications 24h) | 48 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 309 | 0.4541 | 0.3074 | +0.1466 | 🟡+32% | 0.2316 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 180 | 0.4260 | 0.2722 | 0.2189 | 🔴-0.11 | 0.916 |
| S01_NAKAANA1 | win | 83 | 0.4839 | 0.2892 | 0.2471 | 🔴-0.20 | 0.767 |
| S02_TETSUBAN | win | 46 | 0.5103 | 0.4783 | 0.2530 | 🔴-0.01 | 0.876 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.15-0.20 | 5 | 0.1957 | 0.2000 | ✅-0.0043 |
| 0.20-0.30 | 11 | 0.2239 | 0.3636 | 🔴-0.1397 |
| 0.30-0.50 | 140 | 0.4170 | 0.2571 | 🔴+0.1598 |
| 0.50+ | 144 | 0.5400 | 0.3750 | 🔴+0.1650 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 22 | 0.759 |
| win | <5.0 | ✅learned | 40 | 0.808 |
| win | <10.0 | ✅learned | 35 | 0.544 |
| win | <20.0 | ✅learned | 11 | 0.193 |
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
_auto-generated by claude_snapshot.py at 2026-05-26T18:50:01.955600+09:00_