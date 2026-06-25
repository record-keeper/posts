# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-25T11:30:02.622464+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×31 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×31 (24h)
- 🟡 FINAL_MISSING×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-25T11:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-25T11:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-06-25T11:16:41]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×29  [2026-06-25T11:01:37]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×58  [2026-06-25T11:01:37]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×29  [2026-06-25T11:01:37]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×1  [2026-06-25T11:00:37]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-25T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=134<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-25T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=76<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-25T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=21 pred=0.3217 actual=0.2381 gap=+0.0837`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-25T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=32 hit%=21.9% ROI=0.72 (コスト 9,100/回収 6,510)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-25T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1802 actual=0.3750 gap=-0.1948`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-25T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=12 pred=0.2243 actual=0.0833 gap=+0.1410`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-25T06:00:11]
- key: `ROI_STAT|S00: n=158 hit%=25.3% hit_CI[Bonf]=[16.7,36.4]% ROI=0.67 ROI_boot95=[0.47,0.88]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-25T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=158<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-25T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=134 hit%=31.3% hit_CI[Bonf]=[21.2,43.7]% ROI=0.84 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-25T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=76 hit%=32.9% hit_CI[Bonf]=[19.7,49.5]% ROI=0.55 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-25T06:00:11]
- key: `ORPHAN_SCAN|148 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-25T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=22.9% ROI=0.50 (コスト 8,200/回収 4,110)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-25T06:00:11]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=74 hit%=28.4% ROI=0.65 (コスト 17,600/回収 11,430)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.92MB / last modified 2026-06-25T11:30:05.666814+09:00

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
y_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-25 11:29:05,514 [INFO] predictor: Models loaded OK
2026-06-25 11:29:17,907 [INFO] scraper: odds3t: 120/120 parsed
2026-06-25 11:29:18,980 [INFO] scraper: odds3f: 20/20 parsed
2026-06-25 11:29:20,053 [INFO] scraper: odds2t: 30/30 parsed
2026-06-25 11:29:20,054 [INFO] scraper: odds2f: 14/15 parsed
2026-06-25 11:29:21,138 [INFO] scraper: odds_win: 5/6 parsed
2026-06-25 11:29:21,138 [INFO] scraper: fetch_race 18/7: boats=6 odds=189/191
2026-06-25 11:29:21,151 [INFO] predictor: CALIBRATION_MODE=on
2026-06-25 11:29:21,151 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-06-25 11:29:21,163 [INFO] run_cycle: fetched 18/7 [final]: 155 combos
2026-06-25 11:29:24,538 [INFO] scraper: odds3t: 120/120 parsed
2026-06-25 11:29:25,629 [INFO] scraper: odds3f: 20/20 parsed
2026-06-25 11:29:26,729 [INFO] scraper: odds2t: 27/30 parsed
2026-06-25 11:29:26,730 [INFO] scraper: odds2f: 15/15 parsed
2026-06-25 11:29:27,794 [INFO] scraper: odds_win: 6/6 parsed
2026-06-25 11:29:27,794 [INFO] scraper: fetch_race 06/1: boats=6 odds=188/191
2026-06-25 11:29:27,802 [INFO] predictor: CALIBRATION_MODE=on
2026-06-25 11:29:27,802 [INFO] predictor: combos: {'win': 6, '2t': 27, '3t': 120}
2026-06-25 11:29:27,810 [INFO] run_cycle: fetched 06/1 [final]: 153 combos
2026-06-25 11:29:31,340 [INFO] scraper: odds3t: 120/120 parsed
2026-06-25 11:29:32,435 [INFO] scraper: odds3f: 20/20 parsed
2026-06-25 11:29:33,514 [INFO] scraper: odds2t: 27/30 parsed
2026-06-25 11:29:33,515 [INFO] scraper: odds2f: 11/15 parsed
2026-06-25 11:29:34,591 [INFO] scraper: odds_win: 4/6 parsed
2026-06-25 11:29:34,591 [INFO] scraper: fetch_race 09/3: boats=6 odds=182/191
2026-06-25 11:29:34,599 [INFO] predictor: CALIBRATION_MODE=on
2026-06-25 11:29:34,599 [INFO] predictor: combos: {'win': 4, '2t': 27, '3t': 120}
2026-06-25 11:29:34,607 [INFO] run_cycle: fetched 09/3 [scan]: 151 combos
2026-06-25 11:29:34,882 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 55
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 55
  }
]
```

## Phase別通知記録 (24h)
{'final': 22, 'result': 8, 'scan': 25}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 181
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 31
  FINAL_MISSING: 20
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 6
  ANOMALY_BET_VOLUME_DROP: 4
  KS_ODDS_DRIFT: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 47 | 9 | 14,100 | 6,690 | -7,410 | 0.474 |
| S01_NAKAANA1 | 33 | 10 | 6,600 | 5,160 | -1,440 | 0.782 |
| S02_TETSUBAN | 12 | 3 | 2,400 | 1,260 | -1,140 | 0.525 |

## 直近アラート (24h・新しい順)
```
[11:29:34] FINAL_MISSING: {"deadline": "2026-06-25T08:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062521020858", "sid": "S00"}
[11:24:28] CIRCUIT_BREAKER_TRIP: {"cost": 14100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 47, "payout": 6690, "roi_7d": 0.474, "sid": "S00"}
[11:16:41] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.309, "baseline_mean": 0.809, "baseline_stdev": 0.097, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 4, "z_score": -3.18}
[11:01:37] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:01:37] CIRCUIT_BREAKER_TRIP: {"cost": 13800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 46, "payout": 6690, "roi_7d": 0.485, "sid": "S00"}
[11:01:37] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[11:01:37] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[11:00:37] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 2.9, "baseline_n_days": 7, "baseline_stdev": 1.3, "hour": 11, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 0, "z_score": -2.12}
[10:44:28] CIRCUIT_BREAKER_TRIP: {"cost": 13500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 45, "payout": 6690, "roi_7d": 0.496, "sid": "S00"}
[10:29:28] FINAL_MISSING: {"deadline": "2026-06-25T08:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062521020858", "sid": "S00"}
```

## 本日残レース: 160件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 192件 登録 / 32件 締切済
- 通知発射: scan=4 nid / final=4 nid / result=0 nid
- predictions: 2 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 133R | win | 1 | 0.3177 | 13.5 | 4.29 | 300 | scan=- drift=- | 11:24:20 |
| S00 | 132R | win | 1 | 0.6040 | 5.5 | 3.32 | 300 | scan=6.7 drift=-17.9% | 11:01:20 |
| S00 | 227R | win | 1 | 0.5269 | 7.1 | 3.74 | 300 | scan=4.1 drift=+73.2% | 15:35:45 |
| S00 | 048R | win | 1 | 0.5476 | 6.7 | 3.67 | 300 | scan=13.2 drift=-49.2% | 15:29:20 |
| S01_NAKAANA1 | 226R | win | 1 | 0.5990 | 3.6 | 2.16 | 200 | scan=3.5 drift=+2.9% | 15:08:20 |
| S00 | 099R | win | 1 | 0.5123 | 4.2 | 2.15 | 300 | scan=5.4 drift=-22.2% | 14:40:25 |
| S00 | 167R | win | 1 | 0.4111 | 8.2 | 3.37 | 300 | scan=6.0 drift=+36.7% | 14:02:23 |
| S00 | 097R | win | 1 | 0.5735 | 4.8 | 2.75 | 300 | scan=4.1 drift=+17.1% | 13:35:22 |
| S01_NAKAANA1 | 036R | win | 1 | 0.5990 | 3.3 | 1.98 | 200 | scan=3.3 drift=+0.0% | 13:26:33 |
| S00 | 096R | win | 1 | 0.5334 | 6.0 | 3.20 | 300 | scan=5.2 drift=+15.4% | 13:04:40 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 57 | +16.6% | -61.4% | +482.2% | 21 | 8 | 38 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 501.4s |
| **Latency** (scan→final max) | 600.7s |
| **Traffic** (notifications 24h) | 55 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 367 | 0.4752 | 0.2916 | +0.1836 | 🟡+39% | 0.2417 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 157 | 0.4318 | 0.2548 | 0.2262 | 🔴-0.19 | 0.675 |
| S01_NAKAANA1 | win | 134 | 0.4892 | 0.3134 | 0.2437 | 🔴-0.13 | 0.84 |
| S02_TETSUBAN | win | 76 | 0.5400 | 0.3289 | 0.2698 | 🔴-0.22 | 0.553 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1802 | 0.3750 | 🔴-0.1948 |
| 0.20-0.30 | 12 | 0.2243 | 0.0833 | 🔴+0.1410 |
| 0.30-0.50 | 124 | 0.4216 | 0.2419 | 🔴+0.1797 |
| 0.50+ | 216 | 0.5430 | 0.3333 | 🔴+0.2097 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 46 | 0.733 |
| win | <5.0 | ✅learned | 93 | 0.732 |
| win | <10.0 | ✅learned | 57 | 0.496 |
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
_auto-generated by claude_snapshot.py at 2026-06-25T11:30:02.622464+09:00_