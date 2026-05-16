# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-16T14:10:02.126779+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×53 (24h)
- 🔴 PSI_DRIFT_DETECTED×17 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×2 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_BET_VOLUME_DROP  ×8  [2026-05-16T14:02:28]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×8  [2026-05-16T14:02:28]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×8  [2026-05-16T14:02:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×8  [2026-05-16T14:02:28]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🔴 CIRCUIT_BREAKER_TRIP  ×38  [2026-05-16T13:27:51]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×34  [2026-05-16T13:04:40]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-05-16T13:00:09]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×42  [2026-05-16T12:41:02]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×14  [2026-05-16T11:01:21]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-16T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=13 pred=0.0030 actual=0.0769 gap=-0.0739`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-16T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1907 actual=0.1429 gap=+0.0479`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-16T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2234 actual=0.3000 gap=-0.0766`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-16T06:00:09]
- key: `DRIFT_BUCKET|drift ≥+30%: n=33 hit%=21.2% ROI=0.60 (コスト 8,800/回収 5,280)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-16T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=20 pred=0.3268 actual=0.1500 gap=+0.1768`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-16T06:00:09]
- key: `ROI_STAT|S00: n=187 hit%=25.7% hit_CI[Bonf]=[17.6,35.8]% ROI=0.85 ROI_boot95=[0.62,1.10]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-16T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=187<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-16T06:00:09]
- key: `ROI_STAT|S01_NAKAANA1: n=37 hit%=37.8% hit_CI[Bonf]=[19.2,61.0]% ROI=0.76 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-16T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=37<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-16T06:00:09]
- key: `ORPHAN_SCAN|225 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-16T06:00:09]
- key: `DRIFT_BUCKET|drift ≤-30%: n=43 hit%=23.3% ROI=0.61 (コスト 12,700/回収 7,740)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 2.82MB / last modified 2026-05-16T14:09:35.027692+09:00

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
by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-16 14:09:05,430 [INFO] predictor: Models loaded OK
2026-05-16 14:09:17,908 [INFO] scraper: odds3t: 120/120 parsed
2026-05-16 14:09:19,002 [INFO] scraper: odds3f: 20/20 parsed
2026-05-16 14:09:20,133 [INFO] scraper: odds2t: 30/30 parsed
2026-05-16 14:09:20,135 [INFO] scraper: odds2f: 15/15 parsed
2026-05-16 14:09:21,234 [INFO] scraper: odds_win: 6/6 parsed
2026-05-16 14:09:21,234 [INFO] scraper: fetch_race 03/8: boats=6 odds=191/191
2026-05-16 14:09:21,246 [INFO] predictor: CALIBRATION_MODE=on
2026-05-16 14:09:21,246 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-16 14:09:21,253 [INFO] run_cycle: fetched 03/8 [final]: 156 combos
2026-05-16 14:09:24,732 [INFO] scraper: odds3t: 120/120 parsed
2026-05-16 14:09:25,853 [INFO] scraper: odds3f: 20/20 parsed
2026-05-16 14:09:26,945 [INFO] scraper: odds2t: 30/30 parsed
2026-05-16 14:09:26,946 [INFO] scraper: odds2f: 15/15 parsed
2026-05-16 14:09:28,067 [INFO] scraper: odds_win: 6/6 parsed
2026-05-16 14:09:28,067 [INFO] scraper: fetch_race 02/8: boats=6 odds=191/191
2026-05-16 14:09:28,077 [INFO] predictor: CALIBRATION_MODE=on
2026-05-16 14:09:28,077 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-16 14:09:28,085 [INFO] run_cycle: fetched 02/8 [scan]: 156 combos
2026-05-16 14:09:31,509 [INFO] scraper: odds3t: 120/120 parsed
2026-05-16 14:09:32,617 [INFO] scraper: odds3f: 20/20 parsed
2026-05-16 14:09:33,699 [INFO] scraper: odds2t: 30/30 parsed
2026-05-16 14:09:33,700 [INFO] scraper: odds2f: 15/15 parsed
2026-05-16 14:09:34,812 [INFO] scraper: odds_win: 6/6 parsed
2026-05-16 14:09:34,812 [INFO] scraper: fetch_race 21/8: boats=6 odds=191/191
2026-05-16 14:09:34,822 [INFO] predictor: CALIBRATION_MODE=on
2026-05-16 14:09:34,822 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-16 14:09:34,830 [INFO] run_cycle: fetched 21/8 [scan]: 156 combos
2026-05-16 14:09:34,933 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 46
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 46
  }
]
```

## Phase別通知記録 (24h)
{'final': 15, 'result': 7, 'scan': 24}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 165
  FINAL_MISSING: 53
  KS_ODDS_DRIFT: 23
  ANOMALY_SCAN_FINAL_RATIO: 19
  CIRCUIT_BREAKER_NO_ACTION: 18
  PSI_DRIFT_DETECTED: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 4
  CIRCUIT_BREAKER_TRIP: 2
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 48 | 12 | 14,400 | 10,500 | -3,900 | 0.729 |
| S01_NAKAANA1 | 40 | 14 | 8,000 | 5,620 | -2,380 | 0.703 |
| S02_TETSUBAN | 27 | 13 | 5,400 | 5,000 | -400 | 0.926 |

## 直近アラート (24h・新しい順)
```
[14:03:28] FINAL_MISSING: {"deadline": "2026-05-16T11:32:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051617021132", "sid": "S00"}
[14:02:28] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[14:02:28] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[14:00:24] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 11, "baseline_n_days": 7, "baseline_stdev": 2.7, "hour": 14, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 5, "z_score": -2.22}
[13:48:16] FINAL_MISSING: {"deadline": "2026-05-16T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051602021116", "sid": "S00"}
[13:44:41] FINAL_MISSING: {"deadline": "2026-05-16T12:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051602041214", "sid": "S00"}
[13:37:52] FINAL_MISSING: {"deadline": "2026-05-16T13:07:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051614101307", "sid": "S00"}
[13:36:46] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.249, "baseline_mean": 0.715, "baseline_stdev": 0.235, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.467, "today_scan_count": 15, "z_score": -1.06}
[13:34:40] CIRCUIT_BREAKER_TRIP: {"cost": 14400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 48, "payout": 9690, "roi_7d": 0.673, "sid": "S00"}
[13:34:40] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.55}
```

## 本日残レース: 86件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 70件 締切済
- 通知発射: scan=15 nid / final=10 nid / result=5 nid
- predictions: 5 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 8件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 176R | win | 1 | 0.5476 | 15.6 | 8.54 | 300 | scan=22.3 drift=-30.0% | 13:34:31 |
| S01_NAKAANA1 | 042R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=4.3 drift=-18.6% | 12:23:20 |
| S00 | 107R | win | 1 | 0.0295 | 26.0 | 0.77 | 300 | scan=- drift=- | 11:15:33 |
| S01_NAKAANA1 | 021R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=- drift=- | 10:45:22 |
| S01_NAKAANA1 | 142R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=3.3 drift=+0.0% | 09:07:20 |
| S00 | 047R | win | 1 | 0.5735 | 4.1 | 2.35 | 300 | scan=9.3 drift=-55.9% | 14:55:24 |
| S02_TETSUBAN | 038R | win | 1 | 0.4111 | 2.7 | 1.11 | 200 | scan=- drift=- | 14:09:23 |
| S01_NAKAANA1 | 1010R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=3.8 drift=-7.9% | 12:57:22 |
| S02_TETSUBAN | 215R | win | 1 | 0.4111 | 2.4 | 0.99 | 200 | scan=- drift=- | 12:39:46 |
| S01_NAKAANA1 | 108R | win | 1 | 0.4111 | 3.4 | 1.40 | 200 | scan=4.1 drift=-17.1% | 11:56:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 73 | +1.0% | -76.3% | +522.0% | 30 | 15 | 46 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 495.1s |
| **Latency** (scan→final max) | 646.3s |
| **Traffic** (notifications 24h) | 46 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 256 | 0.4517 | 0.2969 | +0.1548 | 🟡+34% | 0.2295 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 189 | 0.4355 | 0.2593 | 0.2250 | 🔴-0.17 | 0.854 |
| S01_NAKAANA1 | win | 40 | 0.4923 | 0.3500 | 0.2350 | 🔴-0.03 | 0.703 |
| S02_TETSUBAN | win | 27 | 0.5049 | 0.4815 | 0.2528 | 🔴-0.01 | 0.926 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 14 | 0.0049 | 0.0714 | 🔴-0.0665 |
| 0.15-0.20 | 7 | 0.1907 | 0.1429 | ✅+0.0479 |
| 0.20-0.30 | 10 | 0.2234 | 0.3000 | 🔴-0.0766 |
| 0.30-0.50 | 118 | 0.4249 | 0.2542 | 🔴+0.1707 |
| 0.50+ | 113 | 0.5413 | 0.3628 | 🔴+0.1784 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 13 | 0.8 |
| win | <5.0 | ✅learned | 28 | 0.706 |
| win | <10.0 | ✅learned | 25 | 0.564 |
| win | <20.0 | ✅learned | 10 | 0.185 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-05-16T14:10:02.126779+09:00_