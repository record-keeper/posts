# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-09T12:50:01.534159+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×48 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×46 (24h)
- 🔴 PSI_DRIFT_DETECTED×38 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×4  [2026-08-09T12:45:36]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×6  [2026-08-09T12:43:04]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-09T12:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-09T12:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 PSI_DRIFT_DETECTED  ×42  [2026-08-09T12:04:22]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 CIRCUIT_BREAKER_TRIP  ×86  [2026-08-09T12:03:30]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×86  [2026-08-09T12:03:30]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×43  [2026-08-09T12:03:30]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×51  [2026-08-09T11:50:44]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ORPHAN_SCAN  ×1  [2026-08-09T06:00:14]
- key: `ORPHAN_SCAN|167 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-09T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=159<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-09T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=10 pred=0.1823 actual=0.2000 gap=-0.0177`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-09T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=12 pred=0.1229 actual=0.1667 gap=-0.0438`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-09T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2237 actual=0.3636 gap=-0.1399`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-09T06:00:14]
- key: `ROI_STAT|S00: n=175 hit%=24.6% hit_CI[Bonf]=[16.5,35.0]% ROI=0.70 ROI_boot95=[0.49,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-09T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=175<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-09T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=159 hit%=24.5% hit_CI[Bonf]=[16.1,35.5]% ROI=0.73 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-09T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=64 hit%=51.6% hit_CI[Bonf]=[34.4,68.3]% ROI=1.00 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-09T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=64<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-09T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=20.6% ROI=0.63 (コスト 10,000/回収 6,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 9.84MB / last modified 2026-08-09T12:49:25.043853+09:00

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
aper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/racelist?rno=5&jcd=16&hd=20260809
2026-08-09 12:48:39,347 [ERROR] scraper: racelist fetch failed: jcd=16 rno=5
2026-08-09 12:48:39,347 [WARNING] run_cycle: fetch None: 16/5
2026-08-09 12:48:50,374 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=13&hd=20260809: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-09 12:49:01,410 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=13&hd=20260809: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-08-09 12:49:14,726 [INFO] scraper: odds3t: 120/120 parsed
2026-08-09 12:49:15,828 [INFO] scraper: odds3f: 20/20 parsed
2026-08-09 12:49:16,907 [INFO] scraper: odds2t: 29/30 parsed
2026-08-09 12:49:16,909 [INFO] scraper: odds2f: 11/15 parsed
2026-08-09 12:49:18,005 [INFO] scraper: odds_win: 6/6 parsed
2026-08-09 12:49:18,006 [INFO] scraper: fetch_race 13/6: boats=6 odds=186/191
2026-08-09 12:49:18,010 [INFO] predictor: CALIBRATION_MODE=on
2026-08-09 12:49:18,010 [INFO] predictor: combos: {'win': 6, '2t': 29, '3t': 120}
2026-08-09 12:49:18,014 [INFO] run_cycle: fetched 13/6 [scan]: 155 combos
2026-08-09 12:49:21,555 [INFO] scraper: odds3t: 120/120 parsed
2026-08-09 12:49:22,625 [INFO] scraper: odds3f: 20/20 parsed
2026-08-09 12:49:23,735 [INFO] scraper: odds2t: 30/30 parsed
2026-08-09 12:49:23,737 [INFO] scraper: odds2f: 15/15 parsed
2026-08-09 12:49:24,828 [INFO] scraper: odds_win: 6/6 parsed
2026-08-09 12:49:24,828 [INFO] scraper: fetch_race 10/10: boats=6 odds=191/191
2026-08-09 12:49:24,831 [INFO] predictor: CALIBRATION_MODE=on
2026-08-09 12:49:24,831 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-09 12:49:24,835 [INFO] run_cycle: fetched 10/10 [scan]: 156 combos
2026-08-09 12:49:24,949 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 78
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 78
  }
]
```

## Phase別通知記録 (24h)
{'final': 28, 'result': 16, 'scan': 34}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 223
  FINAL_MISSING: 48
  CIRCUIT_BREAKER_TRIP: 46
  PSI_DRIFT_DETECTED: 38
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 14
  ANOMALY_BET_VOLUME_SPIKE: 7
  LARGE_ODDS_DRIFT: 2
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 29 | 5 | 8,700 | 4,170 | -4,530 | 0.479 |
| S01_NAKAANA1 | 38 | 7 | 7,600 | 3,720 | -3,880 | 0.489 |
| S02_TETSUBAN | 12 | 7 | 2,400 | 2,240 | -160 | 0.933 |

## 直近アラート (24h・新しい順)
```
[12:49:24] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 325, "n_recent": 79, "psi": 0.3}
[12:49:24] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1155}
[12:47:04] FINAL_MISSING: {"deadline": "2026-08-09T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080902021116", "sid": "S00"}
[12:46:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1183}
[12:45:35] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1178}
[12:45:35] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.119, "baseline_mean": 0.819, "baseline_stdev": 0.056, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.7, "today_scan_count": 20, "z_score": -2.12}
[12:44:03] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 326, "n_recent": 79, "psi": 0.298}
[12:44:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1152}
[12:43:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1185}
[12:42:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1194}
```

## 本日残レース: 110件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 58件 締切済
- 通知発射: scan=20 nid / final=16 nid / result=8 nid
- predictions: 11 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 149R | win | 1 | 0.5123 | 3.5 | 1.79 | 200 | scan=3.0 drift=+16.7% | 12:32:25 |
| S02_TETSUBAN | 053R | win | 1 | 0.5476 | 2.8 | 1.53 | 200 | scan=- drift=- | 12:30:20 |
| S02_TETSUBAN | 135R | win | 1 | 0.5735 | 2.6 | 1.49 | 200 | scan=2.2 drift=+18.2% | 12:24:19 |
| S00 | 238R | win | 1 | 0.4989 | 5.2 | 2.59 | 300 | scan=7.7 drift=-32.5% | 12:14:18 |
| S01_NAKAANA1 | 094R | win | 1 | 0.3177 | 3.2 | 1.02 | 200 | scan=- drift=- | 11:53:30 |
| S01_NAKAANA1 | 023R | win | 1 | 0.5891 | 3.0 | 1.77 | 200 | scan=3.0 drift=+0.0% | 11:42:43 |
| S01_NAKAANA1 | 237R | win | 1 | 0.5476 | 3.4 | 1.86 | 200 | scan=3.0 drift=+13.3% | 11:40:45 |
| S01_NAKAANA1 | 093R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=3.3 drift=+12.1% | 11:22:19 |
| S01_NAKAANA1 | 021R | win | 1 | 0.5735 | 3.0 | 1.72 | 200 | scan=3.5 drift=-14.3% | 10:44:25 |
| S00 | 234R | win | 1 | 0.1957 | 6.9 | 1.35 | 300 | scan=5.2 drift=+32.7% | 10:03:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 48 | -2.3% | -73.3% | +112.5% | 18 | 9 | 36 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 415.3s |
| **Latency** (scan→final max) | 605.5s |
| **Traffic** (notifications 24h) | 78 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 1,200円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 401 | 0.4586 | 0.2843 | +0.1743 | 🟡+38% | 0.2344 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 176 | 0.4109 | 0.2443 | 0.2215 | 🔴-0.20 | 0.699 |
| S01_NAKAANA1 | win | 162 | 0.4830 | 0.2407 | 0.2450 | 🔴-0.34 | 0.717 |
| S02_TETSUBAN | win | 63 | 0.5293 | 0.5079 | 0.2434 | ✅+0.03 | 0.963 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 12 | 0.1229 | 0.1667 | ✅-0.0438 |
| 0.15-0.20 | 11 | 0.1835 | 0.1818 | ✅+0.0017 |
| 0.20-0.30 | 11 | 0.2237 | 0.3636 | 🔴-0.1399 |
| 0.30-0.50 | 155 | 0.4167 | 0.2129 | 🔴+0.2038 |
| 0.50+ | 209 | 0.5410 | 0.3493 | 🔴+0.1918 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 99 | 0.786 |
| win | <5.0 | ✅learned | 174 | 0.723 |
| win | <10.0 | ✅learned | 88 | 0.449 |
| win | <20.0 | ✅learned | 29 | 0.228 |
| win | <50.0 | ⚠️fallback | 6 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-08-09T12:50:01.534159+09:00_