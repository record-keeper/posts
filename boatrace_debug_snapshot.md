# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-05T20:50:02.353607+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×49 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×11 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×22  [2026-07-05T20:28:52]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×38  [2026-07-05T20:12:33]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×43  [2026-07-05T20:07:32]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CIRCUIT_BREAKER_TRIP  ×47  [2026-07-05T20:03:28]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-05T20:00:06]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×24  [2026-07-05T18:27:59]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×19  [2026-07-05T15:48:28]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×11  [2026-07-05T10:01:21]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-05T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=74<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-05T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=140<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-05T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=14 pred=0.2291 actual=0.0714 gap=+0.1577`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-05T06:00:11]
- key: `ROI_STAT|S00: n=169 hit%=27.8% hit_CI[Bonf]=[19.1,38.6]% ROI=0.74 ROI_boot95=[0.54,0.96]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-05T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=169<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-05T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=140 hit%=32.1% hit_CI[Bonf]=[22.0,44.3]% ROI=0.88 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-05T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=74 hit%=35.1% hit_CI[Bonf]=[21.4,51.9]% ROI=0.59 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-07-05T06:00:11]
- key: `ORPHAN_SCAN|161 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-05T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=28.6% ROI=0.88 (コスト 10,200/回収 8,940)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-05T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=42 hit%=23.8% ROI=0.59 (コスト 10,000/回収 5,900)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-05T06:00:11]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=93 hit%=32.3% ROI=0.78 (コスト 21,700/回収 16,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-05T06:00:11]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=26 hit%=34.6% ROI=1.06 (コスト 6,400/回収 6,790)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.86MB / last modified 2026-07-05T20:49:22.014047+09:00

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
FO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-05 20:47:06,926 [INFO] predictor: Models loaded OK
2026-07-05 20:47:07,042 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-05 20:48:06,141 [INFO] run_cycle: === run_cycle 20:48:06 ===
2026-07-05 20:48:06,141 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-05 20:48:06,141 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-05 20:48:06,185 [INFO] predictor: Models loaded OK
2026-07-05 20:48:06,292 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-05 20:49:06,840 [INFO] run_cycle: === run_cycle 20:49:06 ===
2026-07-05 20:49:06,840 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-05 20:49:06,840 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-05 20:49:06,886 [INFO] predictor: Models loaded OK
2026-07-05 20:49:18,354 [INFO] scraper: odds3t: 120/120 parsed
2026-07-05 20:49:19,644 [INFO] scraper: odds3f: 20/20 parsed
2026-07-05 20:49:20,735 [INFO] scraper: odds2t: 30/30 parsed
2026-07-05 20:49:20,736 [INFO] scraper: odds2f: 15/15 parsed
2026-07-05 20:49:21,822 [INFO] scraper: odds_win: 6/6 parsed
2026-07-05 20:49:21,823 [INFO] scraper: fetch_race 24/8: boats=6 odds=191/191
2026-07-05 20:49:21,845 [INFO] predictor: CALIBRATION_MODE=on
2026-07-05 20:49:21,845 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-05 20:49:21,857 [INFO] run_cycle: fetched 24/8 [scan]: 156 combos
2026-07-05 20:49:21,969 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-05 20:50:08,859 [INFO] run_cycle: === run_cycle 20:50:08 ===
2026-07-05 20:50:08,859 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-05 20:50:08,859 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-05 20:50:08,975 [INFO] predictor: Models loaded OK

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
    "c": 91
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 91
  }
]
```

## Phase別通知記録 (24h)
{'final': 39, 'result': 22, 'scan': 30}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 144
  FINAL_MISSING: 49
  ANOMALY_SCAN_FINAL_RATIO: 17
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_NO_ACTION: 15
  CIRCUIT_BREAKER_TRIP: 11
  ANOMALY_BET_VOLUME_DROP: 2
  ANOMALY_BET_VOLUME_SPIKE: 2
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 37 | 10 | 11,100 | 7,500 | -3,600 | 0.676 |
| S01_NAKAANA1 | 39 | 14 | 7,800 | 7,300 | -500 | 0.936 |
| S02_TETSUBAN | 26 | 13 | 5,200 | 4,680 | -520 | 0.9 |

## 直近アラート (24h・新しい順)
```
[20:44:05] FINAL_MISSING: {"deadline": "2026-07-05T14:10:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070509081410", "sid": "S00"}
[20:42:22] FINAL_MISSING: {"deadline": "2026-07-05T14:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070505061409", "sid": "S00"}
[20:28:52] CIRCUIT_BREAKER_TRIP: {"cost": 11100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 7500, "roi_7d": 0.676, "sid": "S00"}
[20:12:33] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[20:07:32] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[20:03:27] FINAL_MISSING: {"deadline": "2026-07-05T16:30:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070501031630", "sid": "S00"}
[20:01:06] FINAL_MISSING: {"deadline": "2026-07-05T17:30:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070501051730", "sid": "S00"}
[20:00:26] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 13.4, "baseline_n_days": 7, "baseline_stdev": 4.1, "hour": 20, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 22, "z_score": 2.08}
[19:43:29] FINAL_MISSING: {"deadline": "2026-07-05T14:10:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070509081410", "sid": "S00"}
[19:42:06] FINAL_MISSING: {"deadline": "2026-07-05T14:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070505061409", "sid": "S00"}
```

## 本日残レース: 5件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 163件 締切済
- 通知発射: scan=27 nid / final=32 nid / result=20 nid
- predictions: 22 / うち結果DB記録済: 22
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 245R | win | 1 | 0.5334 | 10.8 | 5.76 | 300 | scan=- drift=- | 19:27:33 |
| S02_TETSUBAN | 078R | win | 1 | 0.5830 | 2.7 | 1.57 | 200 | scan=2.1 drift=+28.6% | 18:51:46 |
| S01_NAKAANA1 | 015R | win | 1 | 0.3177 | 3.8 | 1.21 | 200 | scan=- drift=- | 17:27:32 |
| S02_TETSUBAN | 1611R | win | 1 | 0.4111 | 2.0 | 0.82 | 200 | scan=2.8 drift=-28.6% | 16:08:22 |
| S01_NAKAANA1 | 011R | win | 1 | 0.3599 | 3.3 | 1.19 | 200 | scan=4.7 drift=-29.8% | 15:22:22 |
| S02_TETSUBAN | 058R | win | 1 | 0.5367 | 2.3 | 1.23 | 200 | scan=- drift=- | 15:03:21 |
| S01_NAKAANA1 | 099R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=- drift=- | 14:37:46 |
| S02_TETSUBAN | 057R | win | 1 | 0.5891 | 2.2 | 1.30 | 200 | scan=- drift=- | 14:33:46 |
| S02_TETSUBAN | 098R | win | 1 | 0.5476 | 2.8 | 1.53 | 200 | scan=- drift=- | 14:07:28 |
| S01_NAKAANA1 | 056R | win | 1 | 0.4111 | 3.8 | 1.56 | 200 | scan=- drift=- | 14:06:52 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 57 | +8.8% | -68.9% | +584.6% | 20 | 5 | 34 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 428.3s |
| **Latency** (scan→final max) | 623.5s |
| **Traffic** (notifications 24h) | 91 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 2,400円 used |
| **Saturation** (S02_TETSUBAN) | 1,200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 394 | 0.4797 | 0.3198 | +0.1599 | 🟡+33% | 0.2391 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 167 | 0.4428 | 0.2874 | 0.2232 | 🔴-0.09 | 0.776 |
| S01_NAKAANA1 | win | 149 | 0.4892 | 0.3221 | 0.2442 | 🔴-0.12 | 0.877 |
| S02_TETSUBAN | win | 78 | 0.5405 | 0.3846 | 0.2632 | 🔴-0.11 | 0.656 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1746 | 0.4286 | 🔴-0.2540 |
| 0.20-0.30 | 14 | 0.2291 | 0.0714 | 🔴+0.1577 |
| 0.30-0.50 | 138 | 0.4217 | 0.2899 | 🔴+0.1318 |
| 0.50+ | 232 | 0.5434 | 0.3534 | 🔴+0.1900 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 61 | 0.748 |
| win | <5.0 | ✅learned | 120 | 0.717 |
| win | <10.0 | ✅learned | 65 | 0.479 |
| win | <20.0 | ✅learned | 19 | 0.212 |
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
_auto-generated by claude_snapshot.py at 2026-07-05T20:50:02.353607+09:00_