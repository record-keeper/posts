# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-26T14:20:02.056586+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×97 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×9 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×15  [2026-05-26T14:05:08]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×19  [2026-05-26T14:00:35]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-05-26T14:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×32  [2026-05-26T13:47:31]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 CIRCUIT_BREAKER_TRIP  ×33  [2026-05-26T13:46:22]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🟡 KS_ODDS_DRIFT  ×10  [2026-05-26T13:36:22]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🔴 PSI_DRIFT_DETECTED  ×53  [2026-05-26T13:26:42]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

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
- DB: 3.56MB / last modified 2026-05-26T14:19:22.446291+09:00

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
2026-05-26 14:17:21,439 [INFO] scraper: odds2t: 30/30 parsed
2026-05-26 14:17:21,440 [INFO] scraper: odds2f: 15/15 parsed
2026-05-26 14:17:22,536 [INFO] scraper: odds_win: 4/6 parsed
2026-05-26 14:17:22,662 [INFO] scraper: fetch_race 03/8: boats=6 odds=189/191
2026-05-26 14:17:22,674 [INFO] predictor: CALIBRATION_MODE=on
2026-05-26 14:17:22,674 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-05-26 14:17:22,681 [INFO] run_cycle: fetched 03/8 [scan]: 154 combos
2026-05-26 14:17:22,795 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-26 14:18:05,449 [INFO] run_cycle: === run_cycle 14:18:05 ===
2026-05-26 14:18:05,450 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-26 14:18:05,450 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-26 14:18:05,527 [INFO] predictor: Models loaded OK
2026-05-26 14:18:05,642 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-26 14:19:05,826 [INFO] run_cycle: === run_cycle 14:19:05 ===
2026-05-26 14:19:05,826 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-26 14:19:05,826 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-26 14:19:05,869 [INFO] predictor: Models loaded OK
2026-05-26 14:19:18,375 [INFO] scraper: odds3t: 120/120 parsed
2026-05-26 14:19:19,492 [INFO] scraper: odds3f: 20/20 parsed
2026-05-26 14:19:20,622 [INFO] scraper: odds2t: 29/30 parsed
2026-05-26 14:19:20,623 [INFO] scraper: odds2f: 15/15 parsed
2026-05-26 14:19:21,750 [INFO] scraper: odds_win: 5/6 parsed
2026-05-26 14:19:21,751 [INFO] scraper: fetch_race 17/8: boats=6 odds=189/191
2026-05-26 14:19:21,761 [INFO] predictor: CALIBRATION_MODE=on
2026-05-26 14:19:21,761 [INFO] predictor: combos: {'win': 5, '2t': 29, '3t': 120}
2026-05-26 14:19:21,769 [INFO] run_cycle: fetched 17/8 [final]: 154 combos
2026-05-26 14:19:21,956 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 38
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 38
  }
]
```

## Phase別通知記録 (24h)
{'final': 14, 'result': 9, 'scan': 15}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 97
  ANOMALY_SCRAPER_FAILURE_BURST: 93
  ANOMALY_SCAN_FINAL_RATIO: 23
  KS_ODDS_DRIFT: 17
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 9
  ANOMALY_BET_VOLUME_DROP: 3
  CIRCUIT_BREAKER_NO_ACTION: 1
  CIRCUIT_BREAKER_TRIP: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 34 | 11 | 10,200 | 10,620 | +420 | 1.041 |
| S01_NAKAANA1 | 32 | 7 | 6,400 | 3,620 | -2,780 | 0.566 |
| S02_TETSUBAN | 14 | 7 | 2,800 | 2,320 | -480 | 0.829 |

## 直近アラート (24h・新しい順)
```
[14:04:28] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[14:00:32] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 8.1, "baseline_n_days": 7, "baseline_stdev": 1.2, "hour": 14, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 5, "z_score": -2.59}
[13:53:36] FINAL_MISSING: {"deadline": "2026-05-26T11:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052610071122", "sid": "S00"}
[13:50:31] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 227, "n_recent": 80, "psi": 0.58}
[13:47:31] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[13:46:22] CIRCUIT_BREAKER_TRIP: {"cost": 6400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 32, "payout": 3620, "roi_7d": 0.566, "sid": "S01_NAKAANA1"}
[13:46:22] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 228, "n_recent": 80, "psi": 0.577}
[13:45:21] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.009125, "ks_stat": 0.209}
[13:45:21] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 227, "n_recent": 81, "psi": 0.581}
[13:39:06] FINAL_MISSING: {"deadline": "2026-05-26T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052603031208", "sid": "S00"}
```

## 本日残レース: 66件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 66件 締切済
- 通知発射: scan=11 nid / final=10 nid / result=5 nid
- predictions: 5 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 1010R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=- drift=- | 12:51:22 |
| S00 | 109R | win | 1 | 0.3177 | 12.9 | 4.10 | 300 | scan=19.1 drift=-32.5% | 12:19:32 |
| S00 | 174R | win | 1 | 0.4111 | 5.7 | 2.34 | 300 | scan=15.0 drift=-62.0% | 12:12:46 |
| S02_TETSUBAN | 032R | win | 1 | 0.5174 | 2.4 | 1.24 | 200 | scan=- drift=- | 11:39:20 |
| S00 | 106R | win | 1 | 0.5123 | 5.0 | 2.56 | 300 | scan=- drift=- | 10:47:22 |
| S01_NAKAANA1 | 1210R | win | 1 | 0.5735 | 3.5 | 2.01 | 200 | scan=- drift=- | 19:39:21 |
| S00 | 126R | win | 1 | 0.5123 | 5.6 | 2.87 | 300 | scan=- drift=- | 17:56:33 |
| S01_NAKAANA1 | 039R | win | 1 | 0.5891 | 3.1 | 1.83 | 200 | scan=3.0 drift=+3.3% | 14:50:24 |
| S02_TETSUBAN | 056R | win | 1 | 0.5226 | 2.0 | 1.05 | 200 | scan=- drift=- | 14:09:21 |
| S00 | 034R | win | 1 | 0.0295 | 5.9 | 0.17 | 300 | scan=14.2 drift=-58.5% | 12:32:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 49 | -3.2% | -78.6% | +157.5% | 20 | 12 | 36 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 541.3s |
| **Latency** (scan→final max) | 672.5s |
| **Traffic** (notifications 24h) | 38 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 307 | 0.4543 | 0.3062 | +0.1482 | 🟡+33% | 0.2314 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 179 | 0.4260 | 0.2737 | 0.2192 | 🔴-0.10 | 0.921 |
| S01_NAKAANA1 | win | 82 | 0.4847 | 0.2805 | 0.2459 | 🔴-0.22 | 0.752 |
| S02_TETSUBAN | win | 46 | 0.5103 | 0.4783 | 0.2530 | 🔴-0.01 | 0.876 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.15-0.20 | 5 | 0.1957 | 0.2000 | ✅-0.0043 |
| 0.20-0.30 | 11 | 0.2239 | 0.3636 | 🔴-0.1397 |
| 0.30-0.50 | 138 | 0.4171 | 0.2536 | 🔴+0.1634 |
| 0.50+ | 144 | 0.5400 | 0.3750 | 🔴+0.1650 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 22 | 0.759 |
| win | <5.0 | ✅learned | 39 | 0.813 |
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
_auto-generated by claude_snapshot.py at 2026-05-26T14:20:02.056586+09:00_