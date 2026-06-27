# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-28T00:50:01.252455+09:00

### 次に取るべきアクション
> RED最優先: CALIBRATION_DRIFT×35 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×93 (24h)
- 🔴 CALIBRATION_DRIFT×35 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×27 (24h)
- 🔴 PSI_DRIFT_DETECTED×23 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-28T00:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-27T23:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×38  [2026-06-27T23:22:06]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 KS_ODDS_DRIFT  ×38  [2026-06-27T23:22:06]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🔴 CALIBRATION_DRIFT  ×52  [2026-06-27T23:08:06]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×52  [2026-06-27T23:08:06]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×104  [2026-06-27T23:08:06]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×52  [2026-06-27T23:08:06]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 PSI_DRIFT_DETECTED  ×60  [2026-06-27T17:24:21]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×61  [2026-06-27T17:00:56]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-06-27T13:52:25]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### 🟡 ANOMALY_BET_VOLUME_DROP  ×58  [2026-06-27T12:00:34]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-27T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=74<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-27T06:00:09]
- key: `ORPHAN_SCAN|149 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-27T06:00:09]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=36 hit%=22.2% ROI=0.47 (コスト 8,500/回収 4,030)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-27T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2250 actual=0.0000 gap=+0.2250`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-27T06:00:09]
- key: `ROI_STAT|S00: n=164 hit%=24.4% hit_CI[Bonf]=[16.1,35.2]% ROI=0.63 ROI_boot95=[0.45,0.83]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-27T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-27T06:00:09]
- key: `ROI_STAT|S01_NAKAANA1: n=145 hit%=30.3% hit_CI[Bonf]=[20.6,42.2]% ROI=0.80 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-27T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=145<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.25MB / last modified 2026-06-28T00:30:11.076896+09:00

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
33 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-27 23:55:06,733 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-27 23:55:06,798 [INFO] predictor: Models loaded OK
2026-06-27 23:55:06,804 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-27 23:56:05,721 [INFO] run_cycle: === run_cycle 23:56:05 ===
2026-06-27 23:56:05,721 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-27 23:56:05,721 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-27 23:56:05,791 [INFO] predictor: Models loaded OK
2026-06-27 23:56:05,799 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-27 23:57:06,207 [INFO] run_cycle: === run_cycle 23:57:06 ===
2026-06-27 23:57:06,207 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-27 23:57:06,207 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-27 23:57:06,257 [INFO] predictor: Models loaded OK
2026-06-27 23:57:06,266 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-27 23:58:05,936 [INFO] run_cycle: === run_cycle 23:58:05 ===
2026-06-27 23:58:05,936 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-27 23:58:05,937 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-27 23:58:06,005 [INFO] predictor: Models loaded OK
2026-06-27 23:58:06,009 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-27 23:59:05,302 [INFO] run_cycle: === run_cycle 23:59:05 ===
2026-06-27 23:59:05,303 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-27 23:59:05,303 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-27 23:59:05,363 [INFO] predictor: Models loaded OK
2026-06-27 23:59:05,369 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 60
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 60
  }
]
```

## Phase別通知記録 (24h)
{'final': 21, 'result': 9, 'scan': 30}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 220
  FINAL_MISSING: 93
  KS_ODDS_DRIFT: 41
  CALIBRATION_DRIFT: 35
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_SCAN_FINAL_RATIO: 30
  CIRCUIT_BREAKER_TRIP: 27
  PSI_DRIFT_DETECTED: 23
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 51 | 10 | 15,300 | 7,170 | -8,130 | 0.469 |
| S01_NAKAANA1 | 30 | 9 | 6,000 | 5,040 | -960 | 0.84 |
| S02_TETSUBAN | 6 | 0 | 1,200 | 0 | -1,200 | 0.0 |

## 直近アラート (24h・新しい順)
```
[23:52:06] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.000328, "ks_stat": 0.252}
[23:52:06] CALIBRATION_DRIFT: {"avg_actual": 0.2184, "avg_pred": 0.4707, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 87, "overconf_pct": 53.6}
[23:51:06] FINAL_MISSING: {"deadline": "2026-06-27T13:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062702061314", "sid": "S00"}
[23:51:06] FINAL_MISSING: {"deadline": "2026-06-27T12:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062702041214", "sid": "S00"}
[23:46:05] FINAL_MISSING: {"deadline": "2026-06-27T17:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062701041712", "sid": "S00"}
[23:42:06] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.21, "baseline_mean": 0.853, "baseline_stdev": 0.067, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.643, "today_scan_count": 28, "z_score": -3.16}
[23:41:05] CIRCUIT_BREAKER_TRIP: {"cost": 15300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 51, "payout": 7170, "roi_7d": 0.469, "sid": "S00"}
[23:30:09] FINAL_MISSING: {"deadline": "2026-06-27T17:56:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062712061756", "sid": "S00"}
[23:26:05] FINAL_MISSING: {"deadline": "2026-06-27T18:52:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062701081852", "sid": "S00"}
[23:25:06] FINAL_MISSING: {"deadline": "2026-06-27T14:48:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062702091448", "sid": "S00"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 0件 登録 / 0件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 1710R | win | 1 | 0.5719 | 5.6 | 3.20 | 300 | scan=8.2 drift=-31.7% | 15:24:21 |
| S00 | 038R | win | 1 | 0.4989 | 17.2 | 8.58 | 300 | scan=5.2 drift=+230.8% | 14:21:41 |
| S00 | 178R | win | 1 | 0.4111 | 5.3 | 2.18 | 300 | scan=- drift=- | 14:21:33 |
| S00 | 028R | win | 1 | 0.4111 | 11.5 | 4.73 | 300 | scan=11.0 drift=+4.5% | 14:13:32 |
| S02_TETSUBAN | 2111R | win | 1 | 0.5334 | 2.2 | 1.17 | 200 | scan=2.6 drift=-15.4% | 13:20:36 |
| S01_NAKAANA1 | 026R | win | 1 | 0.5123 | 3.7 | 1.90 | 200 | scan=3.8 drift=-2.6% | 13:11:27 |
| S00 | 176R | win | 1 | 0.3177 | 9.7 | 3.08 | 300 | scan=9.3 drift=+4.3% | 13:08:21 |
| S00 | 022R | win | 1 | 0.5174 | 4.9 | 2.54 | 300 | scan=10.5 drift=-53.3% | 11:13:21 |
| S00 | 031R | win | 1 | 0.5123 | 4.2 | 2.15 | 300 | scan=- drift=- | 11:11:51 |
| S02_TETSUBAN | 079R | win | 1 | 0.5891 | 2.4 | 1.41 | 200 | scan=- drift=- | 19:22:23 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 51 | +27.7% | -53.3% | +482.2% | 17 | 7 | 34 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 496.0s |
| **Latency** (scan→final max) | 654.8s |
| **Traffic** (notifications 24h) | 60 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 377 | 0.4782 | 0.2732 | +0.2050 | 🟡+43% | 0.2412 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 167 | 0.4395 | 0.2515 | 0.2262 | 🔴-0.20 | 0.649 |
| S01_NAKAANA1 | win | 137 | 0.4909 | 0.2920 | 0.2430 | 🔴-0.18 | 0.78 |
| S02_TETSUBAN | win | 73 | 0.5429 | 0.2877 | 0.2718 | 🔴-0.33 | 0.452 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1819 | 0.3333 | 🔴-0.1514 |
| 0.20-0.30 | 11 | 0.2250 | 0.0000 | 🔴+0.2250 |
| 0.30-0.50 | 126 | 0.4227 | 0.2143 | 🔴+0.2084 |
| 0.50+ | 225 | 0.5434 | 0.3200 | 🔴+0.2234 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 46 | 0.733 |
| win | <5.0 | ✅learned | 98 | 0.729 |
| win | <10.0 | ✅learned | 58 | 0.493 |
| win | <20.0 | ✅learned | 17 | 0.211 |
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
_auto-generated by claude_snapshot.py at 2026-06-28T00:50:01.252455+09:00_