# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-29T15:50:02.118188+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×35 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×48 (24h)
- 🔴 PSI_DRIFT_DETECTED×35 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×24 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×7  [2026-06-29T15:43:32]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-29T15:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×14  [2026-06-29T15:11:58]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×48  [2026-06-29T15:02:42]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×48  [2026-06-29T15:02:42]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×48  [2026-06-29T15:02:42]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 PSI_DRIFT_DETECTED  ×9  [2026-06-29T13:21:38]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 KS_ODDS_DRIFT  ×14  [2026-06-29T12:05:42]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×7  [2026-06-29T10:34:31]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ORPHAN_SCAN  ×1  [2026-06-29T06:00:13]
- key: `ORPHAN_SCAN|154 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-29T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=139<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-29T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=21 pred=0.3217 actual=0.2381 gap=+0.0837`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-29T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1819 actual=0.3333 gap=-0.1514`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-29T06:00:13]
- key: `ROI_STAT|S00: n=163 hit%=27.6% hit_CI[Bonf]=[18.8,38.6]% ROI=0.72 ROI_boot95=[0.52,0.92]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-29T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-29T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=139 hit%=30.2% hit_CI[Bonf]=[20.4,42.3]% ROI=0.80 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-29T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=75 hit%=30.7% hit_CI[Bonf]=[17.9,47.3]% ROI=0.48 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-29T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=75<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-29T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=25.7% ROI=0.83 (コスト 10,100/回収 8,370)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-29T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=22.9% ROI=0.49 (コスト 8,300/回収 4,030)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.43MB / last modified 2026-06-29T15:49:23.484561+09:00

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
d
2026-06-29 15:48:32,918 [INFO] scraper: fetch_race 24/2: boats=6 odds=185/191
2026-06-29 15:48:32,929 [INFO] predictor: CALIBRATION_MODE=on
2026-06-29 15:48:32,930 [INFO] predictor: combos: {'win': 2, '2t': 28, '3t': 120}
2026-06-29 15:48:32,937 [INFO] run_cycle: fetched 24/2 [final]: 150 combos
2026-06-29 15:48:36,545 [INFO] scraper: odds3t: 120/120 parsed
2026-06-29 15:48:37,614 [INFO] scraper: odds3f: 20/20 parsed
2026-06-29 15:48:38,692 [INFO] scraper: odds2t: 30/30 parsed
2026-06-29 15:48:38,693 [INFO] scraper: odds2f: 15/15 parsed
2026-06-29 15:48:39,819 [INFO] scraper: odds_win: 6/6 parsed
2026-06-29 15:48:39,819 [INFO] scraper: fetch_race 02/11: boats=6 odds=191/191
2026-06-29 15:48:39,882 [INFO] predictor: CALIBRATION_MODE=on
2026-06-29 15:48:39,886 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-29 15:48:39,897 [INFO] run_cycle: fetched 02/11 [scan]: 156 combos
2026-06-29 15:48:40,508 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-29 15:49:06,910 [INFO] run_cycle: === run_cycle 15:49:06 ===
2026-06-29 15:49:06,911 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-29 15:49:06,911 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-29 15:49:06,977 [INFO] predictor: Models loaded OK
2026-06-29 15:49:19,455 [INFO] scraper: odds3t: 120/120 parsed
2026-06-29 15:49:20,540 [INFO] scraper: odds3f: 20/20 parsed
2026-06-29 15:49:21,621 [INFO] scraper: odds2t: 28/30 parsed
2026-06-29 15:49:21,622 [INFO] scraper: odds2f: 15/15 parsed
2026-06-29 15:49:22,724 [INFO] scraper: odds_win: 2/6 parsed
2026-06-29 15:49:22,724 [INFO] scraper: fetch_race 24/2: boats=6 odds=185/191
2026-06-29 15:49:22,735 [INFO] predictor: CALIBRATION_MODE=on
2026-06-29 15:49:22,736 [INFO] predictor: combos: {'win': 2, '2t': 28, '3t': 120}
2026-06-29 15:49:22,741 [INFO] run_cycle: fetched 24/2 [final]: 150 combos
2026-06-29 15:49:23,120 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 94
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 94
  }
]
```

## Phase別通知記録 (24h)
{'final': 37, 'result': 19, 'scan': 38}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 151
  FINAL_MISSING: 48
  PSI_DRIFT_DETECTED: 35
  CIRCUIT_BREAKER_TRIP: 24
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 10
  KS_ODDS_DRIFT: 2
  ANOMALY_SCAN_FINAL_RATIO: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 46 | 11 | 13,800 | 8,070 | -5,730 | 0.585 |
| S01_NAKAANA1 | 38 | 17 | 7,600 | 8,520 | +920 | 1.121 |
| S02_TETSUBAN | 9 | 3 | 1,800 | 800 | -1,000 | 0.444 |

## 直近アラート (24h・新しい順)
```
[15:43:31] FINAL_MISSING: {"deadline": "2026-06-29T12:11:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062911041211", "sid": "S00"}
[15:39:36] FINAL_MISSING: {"deadline": "2026-06-29T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062903031208", "sid": "S00"}
[15:31:30] FINAL_MISSING: {"deadline": "2026-06-29T13:00:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062910101300", "sid": "S00"}
[15:30:27] FINAL_MISSING: {"deadline": "2026-06-29T15:00:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062917091500", "sid": "S00"}
[15:28:33] FINAL_MISSING: {"deadline": "2026-06-29T13:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062908081358", "sid": "S00"}
[15:25:39] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 9.4, "baseline_n_days": 7, "baseline_stdev": 2.2, "hour": 15, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 17, "z_score": 3.4}
[15:24:07] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1095}
[15:23:07] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1122}
[15:22:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1118}
[15:21:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1107}
```

## 本日残レース: 58件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 122件 締切済
- 通知発射: scan=29 nid / final=27 nid / result=14 nid
- predictions: 17 / うち結果DB記録済: 15
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 011R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=3.3 drift=-9.1% | 15:25:24 |
| S02_TETSUBAN | 0310R | win | 1 | 0.5174 | 2.6 | 1.35 | 200 | scan=2.4 drift=+8.3% | 15:19:29 |
| S00 | 029R | win | 1 | 0.5334 | 5.0 | 2.67 | 300 | scan=16.1 drift=-68.9% | 14:45:33 |
| S02_TETSUBAN | 119R | win | 1 | 0.5990 | 2.7 | 1.62 | 200 | scan=- drift=- | 14:43:23 |
| S01_NAKAANA1 | 099R | win | 1 | 0.5334 | 3.5 | 1.87 | 200 | scan=- drift=- | 14:40:48 |
| S00 | 117R | win | 1 | 0.5123 | 8.6 | 4.41 | 300 | scan=16.5 drift=-47.9% | 13:40:25 |
| S01_NAKAANA1 | 116R | win | 1 | 0.4111 | 3.9 | 1.60 | 200 | scan=4.5 drift=-13.3% | 13:08:24 |
| S00 | 054R | win | 1 | 0.3177 | 4.0 | 1.27 | 300 | scan=8.5 drift=-52.9% | 13:00:33 |
| S01_NAKAANA1 | 025R | win | 1 | 0.5334 | 3.6 | 1.92 | 200 | scan=4.2 drift=-14.3% | 12:41:23 |
| S00 | 109R | win | 1 | 0.4111 | 4.1 | 1.69 | 300 | scan=5.4 drift=-24.1% | 12:22:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 60 | +7.1% | -68.9% | +325.0% | 25 | 12 | 39 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 487.0s |
| **Latency** (scan→final max) | 617.1s |
| **Traffic** (notifications 24h) | 94 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |
| **Saturation** (S01_NAKAANA1) | 1,600円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 372 | 0.4800 | 0.2984 | +0.1816 | 🟡+38% | 0.2423 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 160 | 0.4398 | 0.2750 | 0.2296 | 🔴-0.15 | 0.731 |
| S01_NAKAANA1 | win | 137 | 0.4915 | 0.3139 | 0.2435 | 🔴-0.13 | 0.838 |
| S02_TETSUBAN | win | 75 | 0.5447 | 0.3200 | 0.2672 | 🔴-0.23 | 0.493 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1819 | 0.3333 | 🔴-0.1514 |
| 0.20-0.30 | 11 | 0.2269 | 0.0909 | 🔴+0.1360 |
| 0.30-0.50 | 127 | 0.4255 | 0.2598 | 🔴+0.1657 |
| 0.50+ | 220 | 0.5448 | 0.3318 | 🔴+0.2129 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 49 | 0.725 |
| win | <5.0 | ✅learned | 108 | 0.72 |
| win | <10.0 | ✅learned | 60 | 0.489 |
| win | <20.0 | ✅learned | 18 | 0.212 |
| win | <50.0 | ⚠️fallback | 2 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-06-29T15:50:02.118188+09:00_