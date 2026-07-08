# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-08T13:10:02.140488+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×20 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×43 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×6  [2026-07-08T13:04:29]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×12  [2026-07-08T13:04:29]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×6  [2026-07-08T13:04:29]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×3  [2026-07-08T13:04:29]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-08T12:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-08T12:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×12  [2026-07-08T12:02:33]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×24  [2026-07-08T11:01:39]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-08T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=74<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-08T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-08T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1746 actual=0.4286 gap=-0.2540`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-08T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=149<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-08T06:00:11]
- key: `ROI_STAT|S00: n=163 hit%=30.7% hit_CI[Bonf]=[21.4,41.8]% ROI=0.80 ROI_boot95=[0.58,1.01]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-08T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=149 hit%=33.6% hit_CI[Bonf]=[23.5,45.3]% ROI=0.92 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-08T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=74 hit%=40.5% hit_CI[Bonf]=[25.8,57.1]% ROI=0.71 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-07-08T06:00:11]
- key: `ORPHAN_SCAN|162 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-08T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=38.2% ROI=1.06 (コスト 9,900/回収 10,470)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-08T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=27.9% ROI=0.67 (コスト 10,100/回収 6,740)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-08T06:00:11]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=94 hit%=33.0% ROI=0.80 (コスト 21,800/回収 17,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-08T06:00:11]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=29 hit%=37.9% ROI=1.08 (コスト 7,200/回収 7,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 7.11MB / last modified 2026-07-08T13:09:06.124029+09:00

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
/20 parsed
2026-07-08 13:07:27,990 [INFO] scraper: odds2t: 30/30 parsed
2026-07-08 13:07:27,991 [INFO] scraper: odds2f: 15/15 parsed
2026-07-08 13:07:29,099 [INFO] scraper: odds_win: 6/6 parsed
2026-07-08 13:07:29,099 [INFO] scraper: fetch_race 11/6: boats=6 odds=191/191
2026-07-08 13:07:29,108 [INFO] predictor: CALIBRATION_MODE=on
2026-07-08 13:07:29,108 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-08 13:07:29,118 [INFO] run_cycle: fetched 11/6 [scan]: 156 combos
2026-07-08 13:07:29,230 [INFO] race_id: notif: nid=2026070811061317 sid=S01_NAKAANA1 phase=scan rank=B
2026-07-08 13:07:29,574 [INFO] notifier: Discord notify OK (status=204)
2026-07-08 13:07:30,236 [INFO] notifier: Discord notify OK (status=204)
2026-07-08 13:07:30,494 [INFO] run_cycle: SCAN S01_NAKAANA1 びわこ6R B
2026-07-08 13:07:30,590 [INFO] run_cycle: run_cycle done: 1 notifications
2026-07-08 13:08:06,191 [INFO] run_cycle: === run_cycle 13:08:06 ===
2026-07-08 13:08:06,191 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-08 13:08:06,191 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-08 13:08:06,234 [INFO] predictor: Models loaded OK
2026-07-08 13:08:06,326 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-08 13:09:05,805 [INFO] run_cycle: === run_cycle 13:09:05 ===
2026-07-08 13:09:05,806 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-08 13:09:05,806 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-08 13:09:05,847 [INFO] predictor: Models loaded OK
2026-07-08 13:09:06,011 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-08 13:10:09,493 [INFO] run_cycle: === run_cycle 13:10:09 ===
2026-07-08 13:10:09,493 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-08 13:10:09,493 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000

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
    "c": 47
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 47
  }
]
```

## Phase別通知記録 (24h)
{'final': 19, 'result': 9, 'scan': 19}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 100
  FINAL_MISSING: 43
  CIRCUIT_BREAKER_NO_ACTION: 34
  KS_ODDS_DRIFT: 31
  CIRCUIT_BREAKER_TRIP: 20
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 8
  ANOMALY_BET_VOLUME_DROP: 3
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 31 | 12 | 9,300 | 8,040 | -1,260 | 0.865 |
| S01_NAKAANA1 | 37 | 9 | 7,400 | 5,160 | -2,240 | 0.697 |
| S02_TETSUBAN | 27 | 14 | 5,400 | 5,440 | +40 | 1.007 |

## 直近アラート (24h・新しい順)
```
[13:04:29] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:04:29] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[13:04:29] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[12:58:44] CIRCUIT_BREAKER_TRIP: {"cost": 7400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 5160, "roi_7d": 0.697, "sid": "S01_NAKAANA1"}
[12:58:44] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.008767, "ks_stat": 0.191}
[12:50:33] FINAL_MISSING: {"deadline": "2026-07-08T10:18:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070810051018", "sid": "S00"}
[12:47:29] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.009621, "ks_stat": 0.189}
[12:43:40] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.222, "baseline_mean": 0.847, "baseline_stdev": 0.098, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.625, "today_scan_count": 8, "z_score": -2.27}
[12:40:32] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.006684, "ks_stat": 0.196}
[12:40:32] FINAL_MISSING: {"deadline": "2026-07-08T11:10:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070811021110", "sid": "S00"}
```

## 本日残レース: 85件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 47件 締切済
- 通知発射: scan=9 nid / final=6 nid / result=2 nid
- predictions: 4 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 1010R | win | 1 | 0.5123 | 6.3 | 3.23 | 300 | scan=5.2 drift=+21.2% | 12:47:20 |
| S02_TETSUBAN | 115R | win | 1 | 0.5123 | 2.1 | 1.08 | 200 | scan=2.1 drift=+0.0% | 12:40:23 |
| S00 | 108R | win | 1 | 0.5123 | 6.2 | 3.18 | 300 | scan=4.3 drift=+44.2% | 11:43:21 |
| S00 | 023R | win | 1 | 0.4920 | 14.3 | 7.04 | 300 | scan=- drift=- | 11:25:20 |
| S01_NAKAANA1 | 248R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=- drift=- | 20:56:46 |
| S01_NAKAANA1 | 014R | win | 1 | 0.3430 | 4.2 | 1.44 | 200 | scan=- drift=- | 17:10:24 |
| S02_TETSUBAN | 204R | win | 1 | 0.4989 | 2.5 | 1.25 | 200 | scan=2.3 drift=+8.7% | 16:57:33 |
| S00 | 203R | win | 1 | 0.4111 | 5.2 | 2.14 | 300 | scan=4.5 drift=+15.6% | 16:20:24 |
| S01_NAKAANA1 | 0510R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=- drift=- | 16:13:32 |
| S02_TETSUBAN | 118R | win | 1 | 0.5998 | 2.2 | 1.32 | 200 | scan=2.1 drift=+4.8% | 14:18:31 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 52 | +2.7% | -52.8% | +200.0% | 14 | 4 | 28 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 348.0s |
| **Latency** (scan→final max) | 660.4s |
| **Traffic** (notifications 24h) | 47 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 385 | 0.4764 | 0.3351 | +0.1414 | 🟡+30% | 0.2357 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 163 | 0.4406 | 0.3067 | 0.2225 | 🔴-0.05 | 0.796 |
| S01_NAKAANA1 | win | 149 | 0.4840 | 0.3356 | 0.2387 | 🔴-0.07 | 0.918 |
| S02_TETSUBAN | win | 73 | 0.5411 | 0.3973 | 0.2591 | 🔴-0.08 | 0.7 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1746 | 0.4286 | 🔴-0.2540 |
| 0.20-0.30 | 13 | 0.2291 | 0.0769 | 🔴+0.1522 |
| 0.30-0.50 | 139 | 0.4178 | 0.3022 | 🔴+0.1156 |
| 0.50+ | 222 | 0.5441 | 0.3739 | 🔴+0.1702 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 63 | 0.76 |
| win | <5.0 | ✅learned | 124 | 0.716 |
| win | <10.0 | ✅learned | 67 | 0.472 |
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
_auto-generated by claude_snapshot.py at 2026-07-08T13:10:02.140488+09:00_