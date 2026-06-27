# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-27T16:50:02.199342+09:00

### 次に取るべきアクション
> RED最優先: CALIBRATION_DRIFT×39 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CALIBRATION_DRIFT×39 (24h)
- 🟡 FINAL_MISSING×34 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×32 (24h)
- 🔴 PSI_DRIFT_DETECTED×19 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-27T16:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-27T16:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 PSI_DRIFT_DETECTED  ×27  [2026-06-27T16:23:59]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 KS_ODDS_DRIFT  ×33  [2026-06-27T16:17:37]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×34  [2026-06-27T16:16:34]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CALIBRATION_DRIFT  ×48  [2026-06-27T16:02:36]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×48  [2026-06-27T16:02:36]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×96  [2026-06-27T16:02:36]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×48  [2026-06-27T16:02:36]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×25  [2026-06-27T15:44:40]
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
- DB: 6.23MB / last modified 2026-06-27T16:49:40.935066+09:00

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
:20,974 [INFO] run_cycle: fetched 17/12 [final]: 155 combos
2026-06-27 16:48:21,240 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-27 16:49:05,926 [INFO] run_cycle: === run_cycle 16:49:05 ===
2026-06-27 16:49:05,926 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-27 16:49:05,926 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-27 16:49:05,967 [INFO] predictor: Models loaded OK
2026-06-27 16:49:17,057 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=17&hd=20260627: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-06-27 16:49:29,713 [INFO] scraper: odds3t: 120/120 parsed
2026-06-27 16:49:30,820 [INFO] scraper: odds3f: 20/20 parsed
2026-06-27 16:49:31,944 [INFO] scraper: odds2t: 30/30 parsed
2026-06-27 16:49:31,945 [INFO] scraper: odds2f: 15/15 parsed
2026-06-27 16:49:33,060 [INFO] scraper: odds_win: 5/6 parsed
2026-06-27 16:49:33,060 [INFO] scraper: fetch_race 17/12: boats=6 odds=190/191
2026-06-27 16:49:33,071 [INFO] predictor: CALIBRATION_MODE=on
2026-06-27 16:49:33,071 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-06-27 16:49:33,079 [INFO] run_cycle: fetched 17/12 [final]: 155 combos
2026-06-27 16:49:36,846 [INFO] scraper: odds3t: 120/120 parsed
2026-06-27 16:49:37,948 [INFO] scraper: odds3f: 20/20 parsed
2026-06-27 16:49:39,377 [INFO] scraper: odds2t: 30/30 parsed
2026-06-27 16:49:39,379 [INFO] scraper: odds2f: 15/15 parsed
2026-06-27 16:49:40,479 [INFO] scraper: odds_win: 4/6 parsed
2026-06-27 16:49:40,479 [INFO] scraper: fetch_race 22/10: boats=6 odds=189/191
2026-06-27 16:49:40,488 [INFO] predictor: CALIBRATION_MODE=on
2026-06-27 16:49:40,488 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-06-27 16:49:40,496 [INFO] run_cycle: fetched 22/10 [scan]: 154 combos
2026-06-27 16:49:40,772 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 75
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 75
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 15, 'scan': 31}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 192
  CALIBRATION_DRIFT: 39
  CIRCUIT_BREAKER_NO_ACTION: 34
  FINAL_MISSING: 34
  CIRCUIT_BREAKER_TRIP: 32
  KS_ODDS_DRIFT: 31
  PSI_DRIFT_DETECTED: 19
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 15
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 51 | 10 | 15,300 | 7,170 | -8,130 | 0.469 |
| S01_NAKAANA1 | 30 | 9 | 6,000 | 5,040 | -960 | 0.84 |
| S02_TETSUBAN | 7 | 0 | 1,400 | 0 | -1,400 | 0.0 |

## 直近アラート (24h・新しい順)
```
[16:47:23] FINAL_MISSING: {"deadline": "2026-06-27T13:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062702061314", "sid": "S00"}
[16:47:23] FINAL_MISSING: {"deadline": "2026-06-27T12:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062702041214", "sid": "S00"}
[16:39:53] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.139, "baseline_mean": 0.853, "baseline_stdev": 0.067, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.714, "today_scan_count": 21, "z_score": -2.09}
[16:36:39] CIRCUIT_BREAKER_TRIP: {"cost": 15300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 51, "payout": 7170, "roi_7d": 0.469, "sid": "S00"}
[16:36:39] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.000415, "ks_stat": 0.246}
[16:36:39] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 294, "n_recent": 88, "psi": 0.265}
[16:36:39] CALIBRATION_DRIFT: {"avg_actual": 0.2159, "avg_pred": 0.4714, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 88, "overconf_pct": 54.2}
[16:29:55] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.187, "baseline_mean": 0.853, "baseline_stdev": 0.067, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 21, "z_score": -2.8}
[16:25:31] CIRCUIT_BREAKER_TRIP: {"cost": 15600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 52, "payout": 7170, "roi_7d": 0.46, "sid": "S00"}
[16:20:55] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.000255, "ks_stat": 0.252}
```

## 本日残レース: 42件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 138件 締切済
- 通知発射: scan=21 nid / final=17 nid / result=9 nid
- predictions: 9 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 7件（FINAL_MISSING の温床）

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
| **Latency** (scan→final avg) | 488.7s |
| **Latency** (scan→final max) | 654.8s |
| **Traffic** (notifications 24h) | 75 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,100円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 382 | 0.4776 | 0.2749 | +0.2027 | 🟡+42% | 0.2405 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 168 | 0.4372 | 0.2500 | 0.2249 | 🔴-0.20 | 0.645 |
| S01_NAKAANA1 | win | 141 | 0.4920 | 0.2979 | 0.2428 | 🔴-0.16 | 0.784 |
| S02_TETSUBAN | win | 73 | 0.5429 | 0.2877 | 0.2718 | 🔴-0.33 | 0.452 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1819 | 0.3333 | 🔴-0.1514 |
| 0.20-0.30 | 11 | 0.2250 | 0.0000 | 🔴+0.2250 |
| 0.30-0.50 | 126 | 0.4227 | 0.2143 | 🔴+0.2084 |
| 0.50+ | 229 | 0.5432 | 0.3231 | 🔴+0.2200 |

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
_auto-generated by claude_snapshot.py at 2026-06-27T16:50:02.199342+09:00_