# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-20T13:40:01.365276+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×21 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×61 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-20T13:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×37  [2026-08-20T13:03:05]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×37  [2026-08-20T13:03:05]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×37  [2026-08-20T13:03:05]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×9  [2026-08-20T12:51:47]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×45  [2026-08-20T11:53:55]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×12  [2026-08-20T11:24:49]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_ODDS_SHIFT  ×24  [2026-08-20T10:59:34]
- key: `ANOMALY_ODDS_SHIFT|`
- **FIX**: odds 分布が2σシフト。scraper format変化・市場変動・戦略filterレンジ変更

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-20T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-20T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=165<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-20T06:00:19]
- key: `ORPHAN_SCAN|194 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-20T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=9 pred=0.1189 actual=0.1111 gap=+0.0078`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-20T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=173<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-20T06:00:19]
- key: `ROI_STAT|S00: n=165 hit%=25.5% hit_CI[Bonf]=[17.0,36.3]% ROI=0.79 ROI_boot95=[0.54,1.08]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-20T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=173 hit%=23.7% hit_CI[Bonf]=[15.7,34.1]% ROI=0.83 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-20T06:00:19]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=44.9% hit_CI[Bonf]=[29.9,60.8]% ROI=0.71 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-20T06:00:19]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=22.9% ROI=0.67 (コスト 10,100/回収 6,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-20T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=32 hit%=37.5% ROI=1.22 (コスト 7,600/回収 9,290)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-20T06:00:19]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=90 hit%=27.8% ROI=0.88 (コスト 20,900/回収 18,410)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-20T06:00:19]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=49 hit%=24.5% ROI=0.48 (コスト 11,300/回収 5,420)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.98MB / last modified 2026-08-20T13:39:27.194623+09:00

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
=== run_cycle 13:38:04 ===
2026-08-20 13:38:04,040 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-20 13:38:04,040 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-20 13:38:04,072 [INFO] predictor: Models loaded OK
2026-08-20 13:38:04,486 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-20 13:39:04,190 [INFO] run_cycle: === run_cycle 13:39:04 ===
2026-08-20 13:39:04,191 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-20 13:39:04,191 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-20 13:39:04,239 [INFO] predictor: Models loaded OK
2026-08-20 13:39:15,669 [INFO] scraper: odds3t: 120/120 parsed
2026-08-20 13:39:16,803 [INFO] scraper: odds3f: 20/20 parsed
2026-08-20 13:39:17,905 [INFO] scraper: odds2t: 30/30 parsed
2026-08-20 13:39:17,906 [INFO] scraper: odds2f: 15/15 parsed
2026-08-20 13:39:19,005 [INFO] scraper: odds_win: 6/6 parsed
2026-08-20 13:39:19,005 [INFO] scraper: fetch_race 02/7: boats=6 odds=191/191
2026-08-20 13:39:19,008 [INFO] predictor: CALIBRATION_MODE=on
2026-08-20 13:39:19,008 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-20 13:39:19,012 [INFO] run_cycle: fetched 02/7 [scan]: 156 combos
2026-08-20 13:39:22,621 [INFO] scraper: odds3t: 120/120 parsed
2026-08-20 13:39:23,726 [INFO] scraper: odds3f: 20/20 parsed
2026-08-20 13:39:24,801 [INFO] scraper: odds2t: 30/30 parsed
2026-08-20 13:39:24,803 [INFO] scraper: odds2f: 15/15 parsed
2026-08-20 13:39:25,881 [INFO] scraper: odds_win: 6/6 parsed
2026-08-20 13:39:25,882 [INFO] scraper: fetch_race 16/7: boats=6 odds=191/191
2026-08-20 13:39:25,884 [INFO] predictor: CALIBRATION_MODE=on
2026-08-20 13:39:25,884 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-20 13:39:25,888 [INFO] run_cycle: fetched 16/7 [scan]: 156 combos
2026-08-20 13:39:26,012 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 82
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 82
  }
]
```

## Phase別通知記録 (24h)
{'final': 31, 'result': 19, 'scan': 32}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 87
  FINAL_MISSING: 61
  CIRCUIT_BREAKER_NO_ACTION: 27
  CIRCUIT_BREAKER_TRIP: 21
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 8
  ANOMALY_BET_VOLUME_SPIKE: 3
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_ODDS_SHIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 50 | 18 | 15,000 | 19,530 | +4,530 | 1.302 |
| S01_NAKAANA1 | 46 | 15 | 9,200 | 12,540 | +3,340 | 1.363 |
| S02_TETSUBAN | 26 | 6 | 5,200 | 1,980 | -3,220 | 0.381 |

## 直近アラート (24h・新しい順)
```
[13:21:28] FINAL_MISSING: {"deadline": "2026-08-20T11:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082021081150", "sid": "S00"}
[13:14:04] FINAL_MISSING: {"deadline": "2026-08-20T12:44:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082002051244", "sid": "S00"}
[13:07:34] CIRCUIT_BREAKER_TRIP: {"cost": 5200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 26, "payout": 1980, "roi_7d": 0.381, "sid": "S02_TETSUBAN"}
[13:07:34] FINAL_MISSING: {"deadline": "2026-08-20T10:37:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082013011037", "sid": "S00"}
[13:03:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:03:04] FINAL_MISSING: {"deadline": "2026-08-20T09:32:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082023030932", "sid": "S00"}
[13:03:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[12:51:46] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 5.3, "baseline_n_days": 7, "baseline_stdev": 2.0, "hour": 12, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 10, "z_score": 2.39}
[12:37:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1255}
[12:36:31] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1229}
```

## 本日残レース: 95件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 73件 締切済
- 通知発射: scan=15 nid / final=15 nid / result=9 nid
- predictions: 11 / うち結果DB記録済: 10
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 044R | win | 1 | 0.5891 | 10.2 | 6.01 | 300 | scan=- drift=- | 13:21:20 |
| S00 | 043R | win | 1 | 0.5123 | 21.0 | 10.76 | 300 | scan=- drift=- | 12:51:31 |
| S01_NAKAANA1 | 165R | win | 1 | 0.5123 | 3.1 | 1.59 | 200 | scan=- drift=- | 12:39:20 |
| S02_TETSUBAN | 164R | win | 1 | 0.5891 | 2.3 | 1.35 | 200 | scan=2.5 drift=-8.0% | 12:07:22 |
| S01_NAKAANA1 | 041R | win | 1 | 0.5990 | 4.2 | 2.52 | 200 | scan=- drift=- | 11:52:21 |
| S00 | 041R | win | 1 | 0.5990 | 4.2 | 2.52 | 300 | scan=8.2 drift=-48.8% | 11:52:20 |
| S02_TETSUBAN | 163R | win | 1 | 0.5891 | 2.3 | 1.35 | 200 | scan=2.6 drift=-11.5% | 11:36:19 |
| S00 | 133R | win | 1 | 0.1760 | 7.9 | 1.39 | 300 | scan=- drift=- | 11:23:18 |
| S00 | 132R | win | 1 | 0.4111 | 12.6 | 5.18 | 300 | scan=14.5 drift=-13.1% | 10:59:31 |
| S00 | 021R | win | 1 | 0.5174 | 36.0 | 18.63 | 300 | scan=10.1 drift=+256.4% | 10:45:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 74 | +9.0% | -62.9% | +256.4% | 16 | 7 | 36 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 509.6s |
| **Latency** (scan→final max) | 650.0s |
| **Traffic** (notifications 24h) | 82 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 419 | 0.4670 | 0.2936 | +0.1735 | 🟡+37% | 0.2401 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 169 | 0.4148 | 0.2663 | 0.2239 | 🔴-0.15 | 0.814 |
| S01_NAKAANA1 | win | 171 | 0.4885 | 0.2456 | 0.2522 | 🔴-0.36 | 0.863 |
| S02_TETSUBAN | win | 79 | 0.5324 | 0.4557 | 0.2486 | 🔴-0.00 | 0.723 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 9 | 0.1189 | 0.1111 | ✅+0.0078 |
| 0.15-0.20 | 12 | 0.1800 | 0.1667 | ✅+0.0134 |
| 0.20-0.30 | 10 | 0.2255 | 0.3000 | 🔴-0.0745 |
| 0.30-0.50 | 152 | 0.4139 | 0.2500 | 🔴+0.1639 |
| 0.50+ | 234 | 0.5433 | 0.3376 | 🔴+0.2056 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 114 | 0.77 |
| win | <5.0 | ✅learned | 203 | 0.757 |
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
_auto-generated by claude_snapshot.py at 2026-08-20T13:40:01.365276+09:00_