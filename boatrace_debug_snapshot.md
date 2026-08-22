# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-22T12:10:01.692368+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×22 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×53 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×6  [2026-08-22T12:04:04]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×6  [2026-08-22T12:04:04]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×6  [2026-08-22T12:04:04]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-22T11:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×28  [2026-08-22T10:51:27]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ORPHAN_SCAN  ×1  [2026-08-22T06:00:47]
- key: `ORPHAN_SCAN|195 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-22T06:00:47]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=82<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-22T06:00:47]
- key: `INSUFFICIENT_SAMPLE|S00: n=173<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-22T06:00:47]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2255 actual=0.3000 gap=-0.0745`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-22T06:00:47]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=12 pred=0.1800 actual=0.1667 gap=+0.0134`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-22T06:00:47]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=34 pred=0.3201 actual=0.3824 gap=-0.0623`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-22T06:00:47]
- key: `ROI_STAT|S00: n=173 hit%=26.6% hit_CI[Bonf]=[18.1,37.2]% ROI=0.81 ROI_boot95=[0.56,1.08]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-22T06:00:47]
- key: `ROI_STAT|S01_NAKAANA1: n=177 hit%=27.1% hit_CI[Bonf]=[18.7,37.6]% ROI=0.87 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-22T06:00:47]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=177<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-22T06:00:47]
- key: `ROI_STAT|S02_TETSUBAN: n=82 hit%=43.9% hit_CI[Bonf]=[29.4,59.5]% ROI=0.71 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-22T06:00:47]
- key: `DRIFT_BUCKET|drift ≤-30%: n=38 hit%=23.7% ROI=0.67 (コスト 11,000/回収 7,340)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-22T06:00:47]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=37 hit%=37.8% ROI=1.00 (コスト 8,700/回収 8,710)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-22T06:00:47]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=92 hit%=28.3% ROI=0.88 (コスト 21,300/回収 18,710)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-22T06:00:47]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=51 hit%=25.5% ROI=0.53 (コスト 11,700/回収 6,180)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-22T06:00:47]
- key: `DRIFT_BUCKET|drift ≥+30%: n=36 hit%=25.0% ROI=1.17 (コスト 10,000/回収 11,710)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.11MB / last modified 2026-08-22T12:09:33.953259+09:00

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
_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-22 12:09:04,690 [INFO] predictor: Models loaded OK
2026-08-22 12:09:16,124 [INFO] scraper: odds3t: 120/120 parsed
2026-08-22 12:09:17,228 [INFO] scraper: odds3f: 20/20 parsed
2026-08-22 12:09:18,303 [INFO] scraper: odds2t: 30/30 parsed
2026-08-22 12:09:18,304 [INFO] scraper: odds2f: 15/15 parsed
2026-08-22 12:09:19,435 [INFO] scraper: odds_win: 6/6 parsed
2026-08-22 12:09:19,435 [INFO] scraper: fetch_race 02/4: boats=6 odds=191/191
2026-08-22 12:09:19,439 [INFO] predictor: CALIBRATION_MODE=on
2026-08-22 12:09:19,439 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-22 12:09:19,443 [INFO] run_cycle: fetched 02/4 [scan]: 156 combos
2026-08-22 12:09:23,041 [INFO] scraper: odds3t: 120/120 parsed
2026-08-22 12:09:24,265 [INFO] scraper: odds3f: 20/20 parsed
2026-08-22 12:09:25,365 [INFO] scraper: odds2t: 26/30 parsed
2026-08-22 12:09:25,366 [INFO] scraper: odds2f: 15/15 parsed
2026-08-22 12:09:26,472 [INFO] scraper: odds_win: 5/6 parsed
2026-08-22 12:09:26,472 [INFO] scraper: fetch_race 22/1: boats=6 odds=186/191
2026-08-22 12:09:26,475 [INFO] predictor: CALIBRATION_MODE=on
2026-08-22 12:09:26,475 [INFO] predictor: combos: {'win': 5, '2t': 26, '3t': 120}
2026-08-22 12:09:26,479 [INFO] run_cycle: fetched 22/1 [scan]: 151 combos
2026-08-22 12:09:30,172 [INFO] scraper: odds3t: 120/120 parsed
2026-08-22 12:09:31,257 [INFO] scraper: odds3f: 20/20 parsed
2026-08-22 12:09:32,374 [INFO] scraper: odds2t: 30/30 parsed
2026-08-22 12:09:32,376 [INFO] scraper: odds2f: 15/15 parsed
2026-08-22 12:09:33,472 [INFO] scraper: odds_win: 6/6 parsed
2026-08-22 12:09:33,472 [INFO] scraper: fetch_race 16/4: boats=6 odds=191/191
2026-08-22 12:09:33,475 [INFO] predictor: CALIBRATION_MODE=on
2026-08-22 12:09:33,475 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-22 12:09:33,479 [INFO] run_cycle: fetched 16/4 [scan]: 156 combos
2026-08-22 12:09:33,604 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 69
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 69
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 16, 'scan': 28}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 111
  FINAL_MISSING: 53
  CIRCUIT_BREAKER_TRIP: 22
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 7
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 41 | 16 | 12,300 | 17,340 | +5,040 | 1.41 |
| S01_NAKAANA1 | 51 | 21 | 10,200 | 14,020 | +3,820 | 1.375 |
| S02_TETSUBAN | 28 | 7 | 5,600 | 2,620 | -2,980 | 0.468 |

## 直近アラート (24h・新しい順)
```
[12:03:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:03:03] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[11:56:44] CIRCUIT_BREAKER_TRIP: {"cost": 5600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 28, "payout": 2620, "roi_7d": 0.468, "sid": "S02_TETSUBAN"}
[11:43:26] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.248, "baseline_mean": 0.82, "baseline_stdev": 0.1, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.571, "today_scan_count": 7, "z_score": -2.49}
[11:17:30] FINAL_MISSING: {"deadline": "2026-08-22T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082202011047", "sid": "S00"}
[11:11:30] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.22, "baseline_mean": 0.82, "baseline_stdev": 0.1, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.6, "today_scan_count": 5, "z_score": -2.2}
[11:07:30] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.42, "baseline_mean": 0.82, "baseline_stdev": 0.1, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.4, "today_scan_count": 5, "z_score": -4.21}
[11:02:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:02:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[11:01:22] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.32, "baseline_mean": 0.82, "baseline_stdev": 0.1, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 4, "z_score": -3.21}
```

## 本日残レース: 124件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 32件 締切済
- 通知発射: scan=8 nid / final=6 nid / result=2 nid
- predictions: 3 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 218R | win | 1 | 0.5123 | 4.6 | 2.36 | 200 | scan=3.0 drift=+53.3% | 11:48:44 |
| S01_NAKAANA1 | 236R | win | 1 | 0.4989 | 4.3 | 2.15 | 200 | scan=3.4 drift=+26.5% | 10:58:20 |
| S02_TETSUBAN | 212R | win | 1 | 0.5990 | 2.6 | 1.56 | 200 | scan=2.0 drift=+30.0% | 08:55:19 |
| S01_NAKAANA1 | 246R | win | 1 | 0.5174 | 3.6 | 1.86 | 200 | scan=- drift=- | 19:53:19 |
| S01_NAKAANA1 | 074R | win | 1 | 0.5735 | 4.3 | 2.47 | 200 | scan=- drift=- | 16:37:32 |
| S00 | 074R | win | 1 | 0.5735 | 4.3 | 2.47 | 300 | scan=7.1 drift=-39.4% | 16:37:30 |
| S01_NAKAANA1 | 048R | win | 1 | 0.5334 | 3.4 | 1.81 | 200 | scan=4.6 drift=-26.1% | 15:28:19 |
| S01_NAKAANA1 | 151R | win | 1 | 0.5334 | 3.5 | 1.87 | 200 | scan=3.0 drift=+16.7% | 15:15:32 |
| S02_TETSUBAN | 168R | win | 1 | 0.4989 | 2.3 | 1.15 | 200 | scan=2.8 drift=-17.9% | 14:30:34 |
| S01_NAKAANA1 | 065R | win | 1 | 0.5891 | 4.3 | 2.53 | 200 | scan=3.0 drift=+43.3% | 13:34:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 75 | +5.1% | -56.0% | +256.4% | 20 | 8 | 42 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 506.8s |
| **Latency** (scan→final max) | 610.9s |
| **Traffic** (notifications 24h) | 69 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 430 | 0.4682 | 0.3000 | +0.1682 | 🟡+36% | 0.2397 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 172 | 0.4152 | 0.2674 | 0.2230 | 🔴-0.14 | 0.813 |
| S01_NAKAANA1 | win | 177 | 0.4902 | 0.2712 | 0.2496 | 🔴-0.26 | 0.868 |
| S02_TETSUBAN | win | 81 | 0.5327 | 0.4321 | 0.2537 | 🔴-0.03 | 0.69 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1219 | 0.1000 | ✅+0.0219 |
| 0.15-0.20 | 12 | 0.1800 | 0.1667 | ✅+0.0134 |
| 0.20-0.30 | 10 | 0.2255 | 0.3000 | 🔴-0.0745 |
| 0.30-0.50 | 153 | 0.4131 | 0.2549 | 🔴+0.1581 |
| 0.50+ | 243 | 0.5446 | 0.3457 | 🔴+0.1989 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 116 | 0.772 |
| win | <5.0 | ✅learned | 212 | 0.75 |
| win | <10.0 | ✅learned | 101 | 0.456 |
| win | <20.0 | ✅learned | 30 | 0.227 |
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
_auto-generated by claude_snapshot.py at 2026-08-22T12:10:01.692368+09:00_