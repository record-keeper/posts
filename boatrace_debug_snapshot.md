# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-19T10:40:02.200575+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×23 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×31 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×23 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×38  [2026-05-19T10:02:05]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×38  [2026-05-19T10:02:05]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×38  [2026-05-19T10:02:05]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×38  [2026-05-19T10:02:05]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_BET_VOLUME_DROP  ×15  [2026-05-19T10:00:26]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-05-19T09:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-19T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1907 actual=0.1429 gap=+0.0479`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-19T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=44 hit%=25.0% ROI=0.66 (コスト 13,000/回収 8,550)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-19T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=14 pred=0.0049 actual=0.0714 gap=-0.0665`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-19T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=193<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-19T06:00:11]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=20 hit%=35.0% ROI=1.00 (コスト 5,400/回収 5,400)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-19T06:00:11]
- key: `DRIFT_BUCKET|drift ≥+30%: n=35 hit%=22.9% ROI=0.66 (コスト 9,200/回収 6,080)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-19T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2239 actual=0.3636 gap=-0.1397`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-19T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=21 pred=0.3263 actual=0.1429 gap=+0.1835`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-19T06:00:11]
- key: `ROI_STAT|S00: n=193 hit%=26.4% hit_CI[Bonf]=[18.4,36.4]% ROI=0.87 ROI_boot95=[0.63,1.12]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-19T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=46 hit%=32.6% hit_CI[Bonf]=[16.7,53.8]% ROI=0.70 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-19T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=46<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-19T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=32 hit%=46.9% hit_CI[Bonf]=[24.8,70.2]% ROI=0.90 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-19T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=32<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-19T06:00:11]
- key: `ORPHAN_SCAN|240 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 2.95MB / last modified 2026-05-19T10:39:23.120297+09:00

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
rsed
2026-05-19 10:38:19,903 [INFO] scraper: fetch_race 21/1: boats=6 odds=191/191
2026-05-19 10:38:19,915 [INFO] predictor: CALIBRATION_MODE=on
2026-05-19 10:38:19,915 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-19 10:38:19,922 [INFO] run_cycle: fetched 21/1 [final]: 156 combos
2026-05-19 10:38:23,539 [INFO] scraper: odds3t: 120/120 parsed
2026-05-19 10:38:24,647 [INFO] scraper: odds3f: 20/20 parsed
2026-05-19 10:38:25,755 [INFO] scraper: odds2t: 30/30 parsed
2026-05-19 10:38:25,756 [INFO] scraper: odds2f: 14/15 parsed
2026-05-19 10:38:26,830 [INFO] scraper: odds_win: 1/6 parsed
2026-05-19 10:38:26,830 [INFO] scraper: fetch_race 14/6: boats=6 odds=185/191
2026-05-19 10:38:26,840 [INFO] predictor: CALIBRATION_MODE=on
2026-05-19 10:38:26,840 [INFO] predictor: combos: {'win': 1, '2t': 30, '3t': 120}
2026-05-19 10:38:26,848 [INFO] run_cycle: fetched 14/6 [scan]: 151 combos
2026-05-19 10:38:26,976 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-19 10:39:06,304 [INFO] run_cycle: === run_cycle 10:39:06 ===
2026-05-19 10:39:06,304 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-19 10:39:06,304 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-19 10:39:06,356 [INFO] predictor: Models loaded OK
2026-05-19 10:39:18,922 [INFO] scraper: odds3t: 120/120 parsed
2026-05-19 10:39:20,076 [INFO] scraper: odds3f: 20/20 parsed
2026-05-19 10:39:21,211 [INFO] scraper: odds2t: 27/30 parsed
2026-05-19 10:39:21,212 [INFO] scraper: odds2f: 12/15 parsed
2026-05-19 10:39:22,347 [INFO] scraper: odds_win: 5/6 parsed
2026-05-19 10:39:22,347 [INFO] scraper: fetch_race 17/1: boats=6 odds=184/191
2026-05-19 10:39:22,359 [INFO] predictor: CALIBRATION_MODE=on
2026-05-19 10:39:22,359 [INFO] predictor: combos: {'win': 5, '2t': 27, '3t': 120}
2026-05-19 10:39:22,367 [INFO] run_cycle: fetched 17/1 [scan]: 152 combos
2026-05-19 10:39:22,602 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 31
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 31
  }
]
```

## Phase別通知記録 (24h)
{'final': 12, 'result': 4, 'scan': 15}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 87
  KS_ODDS_DRIFT: 37
  FINAL_MISSING: 31
  CIRCUIT_BREAKER_TRIP: 23
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 4
  ANOMALY_SCAN_FINAL_RATIO: 4
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 37 | 11 | 11,100 | 9,240 | -1,860 | 0.832 |
| S01_NAKAANA1 | 32 | 9 | 6,400 | 3,880 | -2,520 | 0.606 |
| S02_TETSUBAN | 19 | 9 | 3,800 | 3,100 | -700 | 0.816 |

## 直近アラート (24h・新しい順)
```
[10:32:05] CIRCUIT_BREAKER_TRIP: {"cost": 6400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 32, "payout": 3880, "roi_7d": 0.606, "sid": "S01_NAKAANA1"}
[10:32:05] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.451}
[10:15:23] CIRCUIT_BREAKER_TRIP: {"cost": 6600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 33, "payout": 4220, "roi_7d": 0.639, "sid": "S01_NAKAANA1"}
[10:15:23] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.457}
[10:12:21] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.454}
[10:02:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:02:05] CIRCUIT_BREAKER_TRIP: {"cost": 6400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 32, "payout": 4220, "roi_7d": 0.659, "sid": "S01_NAKAANA1"}
[10:02:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[10:00:26] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 1.4, "baseline_n_days": 7, "baseline_stdev": 0.5, "hour": 10, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 0, "z_score": -2.67}
[09:12:06] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.454}
```

## 本日残レース: 120件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 12件 締切済
- 通知発射: scan=2 nid / final=1 nid / result=0 nid
- predictions: 1 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 145R | win | 1 | 0.4989 | 4.2 | 2.10 | 200 | scan=4.0 drift=+5.0% | 10:15:21 |
| S02_TETSUBAN | 2012R | win | 1 | 0.5334 | 2.2 | 1.17 | 200 | scan=2.2 drift=+0.0% | 22:51:33 |
| S01_NAKAANA1 | 153R | win | 1 | 0.5123 | 3.8 | 1.95 | 200 | scan=- drift=- | 16:31:45 |
| S02_TETSUBAN | 215R | win | 1 | 0.5735 | 2.3 | 1.32 | 200 | scan=2.6 drift=-11.5% | 12:35:22 |
| S01_NAKAANA1 | 149R | win | 1 | 0.5334 | 3.7 | 1.97 | 200 | scan=- drift=- | 12:23:22 |
| S00 | 142R | win | 1 | 0.4111 | 8.8 | 3.62 | 300 | scan=- drift=- | 09:03:21 |
| S02_TETSUBAN | 209R | win | 1 | 0.5334 | 2.5 | 1.33 | 200 | scan=2.4 drift=+4.2% | 21:25:22 |
| S00 | 155R | win | 1 | 0.2290 | 11.6 | 2.66 | 300 | scan=- drift=- | 17:34:32 |
| S01_NAKAANA1 | 154R | win | 1 | 0.5123 | 3.3 | 1.69 | 200 | scan=- drift=- | 17:11:21 |
| S00 | 153R | win | 1 | 0.5735 | 27.0 | 15.48 | 300 | scan=- drift=- | 16:34:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 54 | +7.5% | -76.3% | +522.0% | 18 | 9 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 569.6s |
| **Latency** (scan→final max) | 602.4s |
| **Traffic** (notifications 24h) | 31 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 271 | 0.4538 | 0.2989 | +0.1549 | 🟡+34% | 0.2316 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 193 | 0.4355 | 0.2642 | 0.2273 | 🔴-0.17 | 0.869 |
| S01_NAKAANA1 | win | 46 | 0.4925 | 0.3261 | 0.2365 | 🔴-0.08 | 0.698 |
| S02_TETSUBAN | win | 32 | 0.5085 | 0.4688 | 0.2502 | 🔴-0.00 | 0.897 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 14 | 0.0049 | 0.0714 | 🔴-0.0665 |
| 0.15-0.20 | 7 | 0.1907 | 0.1429 | ✅+0.0479 |
| 0.20-0.30 | 11 | 0.2239 | 0.3636 | 🔴-0.1397 |
| 0.30-0.50 | 121 | 0.4246 | 0.2479 | 🔴+0.1767 |
| 0.50+ | 124 | 0.5406 | 0.3629 | 🔴+0.1777 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 15 | 0.795 |
| win | <5.0 | ✅learned | 29 | 0.715 |
| win | <10.0 | ✅learned | 26 | 0.556 |
| win | <20.0 | ✅learned | 11 | 0.193 |
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
_auto-generated by claude_snapshot.py at 2026-05-19T10:40:02.200575+09:00_