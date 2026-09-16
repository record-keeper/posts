# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-16T16:20:02.110876+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×57 (24h) → ログ/DB確認

### 検出された問題
- 🔴 PSI_DRIFT_DETECTED×57 (24h)
- 🟡 FINAL_MISSING×56 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×48 (24h)
- 🔴 CALIBRATION_DRIFT×33 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×3 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×24  [2026-09-16T16:08:30]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×24  [2026-09-16T16:08:30]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×12  [2026-09-16T16:08:30]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×12  [2026-09-16T16:08:30]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CALIBRATION_DRIFT  ×10  [2026-09-16T15:35:30]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-16T15:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-16T15:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×50  [2026-09-16T12:31:11]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-09-16T12:20:53]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### 🟡 ANOMALY_ODDS_SHIFT  ×28  [2026-09-16T10:52:37]
- key: `ANOMALY_ODDS_SHIFT|`
- **FIX**: odds 分布が2σシフト。scraper format変化・市場変動・戦略filterレンジ変更

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-09-16T10:44:52]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-16T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-16T06:00:12]
- key: `ORPHAN_SCAN|171 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-16T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=173<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-16T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1314 actual=0.0000 gap=+0.1314`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-16T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1783 actual=0.3333 gap=-0.1550`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-16T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=7 pred=0.2214 actual=0.0000 gap=+0.2214`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-16T06:00:12]
- key: `ROI_STAT|S00: n=173 hit%=27.2% hit_CI[Bonf]=[18.6,37.8]% ROI=0.94 ROI_boot95=[0.66,1.26]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-16T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=174 hit%=24.7% hit_CI[Bonf]=[16.6,35.2]% ROI=0.76 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-16T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=174<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.4MB / last modified 2026-09-16T16:19:45.241559+09:00

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
 parsed
2026-09-16 16:18:19,544 [INFO] scraper: odds2f: 14/15 parsed
2026-09-16 16:18:20,626 [INFO] scraper: odds_win: 3/6 parsed
2026-09-16 16:18:20,626 [INFO] scraper: fetch_race 09/12: boats=6 odds=187/191
2026-09-16 16:18:20,634 [INFO] predictor: CALIBRATION_MODE=on
2026-09-16 16:18:20,634 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-09-16 16:18:20,638 [INFO] run_cycle: fetched 09/12 [final]: 153 combos
2026-09-16 16:18:21,236 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-16 16:19:04,834 [INFO] run_cycle: === run_cycle 16:19:04 ===
2026-09-16 16:19:04,834 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-16 16:19:04,834 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-16 16:19:04,882 [INFO] predictor: Models loaded OK
2026-09-16 16:19:15,957 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=08&hd=20260916: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-09-16 16:19:27,015 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=08&hd=20260916: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-09-16 16:19:40,506 [INFO] scraper: odds3t: 120/120 parsed
2026-09-16 16:19:41,656 [INFO] scraper: odds3f: 20/20 parsed
2026-09-16 16:19:42,731 [INFO] scraper: odds2t: 30/30 parsed
2026-09-16 16:19:42,732 [INFO] scraper: odds2f: 15/15 parsed
2026-09-16 16:19:43,806 [INFO] scraper: odds_win: 6/6 parsed
2026-09-16 16:19:43,806 [INFO] scraper: fetch_race 08/12: boats=6 odds=191/191
2026-09-16 16:19:43,810 [INFO] predictor: CALIBRATION_MODE=on
2026-09-16 16:19:43,811 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-16 16:19:43,817 [INFO] run_cycle: fetched 08/12 [scan]: 156 combos
2026-09-16 16:19:44,129 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 93
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 93
  }
]
```

## Phase別通知記録 (24h)
{'final': 36, 'result': 21, 'scan': 36}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 71
  PSI_DRIFT_DETECTED: 57
  FINAL_MISSING: 56
  CIRCUIT_BREAKER_TRIP: 48
  CIRCUIT_BREAKER_NO_ACTION: 34
  CALIBRATION_DRIFT: 33
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 3
  LARGE_ODDS_DRIFT: 3
  ANOMALY_ODDS_SHIFT: 2
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 8 | 10,800 | 6,720 | -4,080 | 0.622 |
| S01_NAKAANA1 | 34 | 8 | 6,800 | 4,660 | -2,140 | 0.685 |
| S02_TETSUBAN | 16 | 5 | 3,200 | 1,360 | -1,840 | 0.425 |

## 直近アラート (24h・新しい順)
```
[16:19:44] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 343, "n_recent": 86, "psi": 0.707}
[16:18:21] FINAL_MISSING: {"deadline": "2026-09-16T15:48:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091607021548", "sid": "S00"}
[16:16:34] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 344, "n_recent": 86, "psi": 0.702}
[16:12:37] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 345, "n_recent": 86, "psi": 0.701}
[16:10:36] CIRCUIT_BREAKER_TRIP: {"cost": 10500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 6720, "roi_7d": 0.64, "sid": "S00"}
[16:10:36] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 345, "n_recent": 85, "psi": 0.706}
[16:08:27] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[16:08:27] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[16:08:27] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[15:57:37] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 343, "n_recent": 87, "psi": 0.735}
```

## 本日残レース: 34件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 122件 締切済
- 通知発射: scan=23 nid / final=24 nid / result=15 nid
- predictions: 18 / うち結果DB記録済: 17
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 073R | win | 1 | 0.5476 | 10.5 | 5.75 | 300 | scan=5.6 drift=+87.5% | 16:12:19 |
| S01_NAKAANA1 | 072R | win | 1 | 0.5174 | 4.0 | 2.07 | 200 | scan=3.3 drift=+21.2% | 15:45:18 |
| S00 | 191R | win | 1 | 0.4989 | 6.6 | 3.29 | 300 | scan=12.7 drift=-48.0% | 15:20:31 |
| S00 | 121R | win | 1 | 0.4111 | 18.7 | 7.69 | 300 | scan=18.7 drift=+0.0% | 15:14:19 |
| S00 | 1310R | win | 1 | 0.5519 | 4.1 | 2.26 | 300 | scan=5.2 drift=-21.2% | 15:02:18 |
| S01_NAKAANA1 | 098R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=- drift=- | 14:05:22 |
| S01_NAKAANA1 | 138R | win | 1 | 0.4989 | 3.7 | 1.85 | 200 | scan=3.0 drift=+23.3% | 13:54:24 |
| S00 | 137R | win | 1 | 0.4989 | 5.2 | 2.59 | 300 | scan=5.2 drift=+0.0% | 13:24:19 |
| S02_TETSUBAN | 056R | win | 1 | 0.5123 | 2.0 | 1.02 | 200 | scan=2.4 drift=-16.7% | 12:54:19 |
| S00 | 222R | win | 1 | 0.5123 | 9.0 | 4.61 | 300 | scan=4.1 drift=+119.5% | 12:11:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 55 | +7.5% | -80.2% | +119.5% | 13 | 3 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 471.4s |
| **Latency** (scan→final max) | 615.3s |
| **Traffic** (notifications 24h) | 93 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 3,300円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 428 | 0.4765 | 0.2687 | +0.2078 | 🟡+44% | 0.2440 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 176 | 0.4372 | 0.2727 | 0.2315 | 🔴-0.17 | 0.948 |
| S01_NAKAANA1 | win | 175 | 0.4859 | 0.2343 | 0.2465 | 🔴-0.37 | 0.721 |
| S02_TETSUBAN | win | 77 | 0.5451 | 0.3377 | 0.2670 | 🔴-0.19 | 0.603 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1314 | 0.0000 | 🔴+0.1314 |
| 0.15-0.20 | 6 | 0.1783 | 0.3333 | 🔴-0.1550 |
| 0.20-0.30 | 6 | 0.2221 | 0.0000 | 🔴+0.2221 |
| 0.30-0.50 | 152 | 0.4074 | 0.2303 | 🔴+0.1771 |
| 0.50+ | 254 | 0.5454 | 0.2992 | 🔴+0.2462 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 138 | 0.766 |
| win | <5.0 | ✅learned | 251 | 0.753 |
| win | <10.0 | ✅learned | 122 | 0.466 |
| win | <20.0 | ✅learned | 33 | 0.234 |
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
_auto-generated by claude_snapshot.py at 2026-09-16T16:20:02.110876+09:00_