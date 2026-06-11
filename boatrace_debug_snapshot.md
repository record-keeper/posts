# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-11T13:00:02.011133+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×73 (24h)
- 🔴 CALIBRATION_DRIFT×32 (24h)
- 🟡 FINAL_MISSING×30 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×3  [2026-06-11T12:43:56]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×55  [2026-06-11T12:05:54]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🔴 CALIBRATION_DRIFT  ×47  [2026-06-11T12:03:42]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×171  [2026-06-11T12:03:42]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×171  [2026-06-11T12:03:42]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×57  [2026-06-11T12:03:42]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×2  [2026-06-11T12:01:50]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-11T12:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-11T12:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-11T12:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-11T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1254 actual=0.1667 gap=-0.0412`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-11T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=6 pred=0.2216 actual=0.3333 gap=-0.1117`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-11T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1918 actual=0.2000 gap=-0.0082`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-11T06:00:11]
- key: `ORPHAN_SCAN|142 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ ROI_STAT  ×1  [2026-06-11T06:00:11]
- key: `ROI_STAT|S00: n=149 hit%=25.5% hit_CI[Bonf]=[16.7,36.9]% ROI=0.76 ROI_boot95=[0.50,1.06]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-11T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=149<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-11T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=138 hit%=28.3% hit_CI[Bonf]=[18.7,40.3]% ROI=0.71 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-11T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=138<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-11T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=36.2% hit_CI[Bonf]=[22.7,52.4]% ROI=0.61 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-11T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.82MB / last modified 2026-06-11T13:00:04.745611+09:00

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
default=100
2026-06-11 12:59:05,915 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-11 12:59:05,988 [INFO] predictor: Models loaded OK
2026-06-11 12:59:17,038 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=5&jcd=03&hd=20260611: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-06-11 12:59:28,495 [INFO] scraper: odds3t: 120/120 parsed
2026-06-11 12:59:29,596 [INFO] scraper: odds3f: 20/20 parsed
2026-06-11 12:59:30,715 [INFO] scraper: odds2t: 30/30 parsed
2026-06-11 12:59:30,716 [INFO] scraper: odds2f: 13/15 parsed
2026-06-11 12:59:31,859 [INFO] scraper: odds_win: 4/6 parsed
2026-06-11 12:59:31,859 [INFO] scraper: fetch_race 03/5: boats=6 odds=187/191
2026-06-11 12:59:31,871 [INFO] predictor: CALIBRATION_MODE=on
2026-06-11 12:59:31,871 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-06-11 12:59:31,880 [INFO] run_cycle: fetched 03/5 [final]: 154 combos
2026-06-11 12:59:32,825 [INFO] race_id: notif: nid=2026061103051302 sid=S00 phase=final rank=S
2026-06-11 12:59:33,274 [INFO] notifier: Discord notify OK (status=204)
2026-06-11 12:59:35,160 [INFO] notifier: Discord notify OK (status=204)
2026-06-11 12:59:35,166 [INFO] run_cycle: FINAL S00 江戸川5R S
2026-06-11 12:59:38,843 [INFO] scraper: odds3t: 120/120 parsed
2026-06-11 12:59:39,975 [INFO] scraper: odds3f: 20/20 parsed
2026-06-11 12:59:41,064 [INFO] scraper: odds2t: 30/30 parsed
2026-06-11 12:59:41,065 [INFO] scraper: odds2f: 14/15 parsed
2026-06-11 12:59:42,208 [INFO] scraper: odds_win: 3/6 parsed
2026-06-11 12:59:42,208 [INFO] scraper: fetch_race 14/10: boats=6 odds=187/191
2026-06-11 12:59:42,216 [INFO] predictor: CALIBRATION_MODE=on
2026-06-11 12:59:42,218 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-06-11 12:59:42,226 [INFO] run_cycle: fetched 14/10 [scan]: 153 combos
2026-06-11 12:59:42,449 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 76
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 76
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 18, 'scan': 29}

## アラート件数 (24h・種類別)
```
  CIRCUIT_BREAKER_TRIP: 73
  CIRCUIT_BREAKER_NO_ACTION: 51
  ANOMALY_SCRAPER_FAILURE_BURST: 33
  CALIBRATION_DRIFT: 32
  FINAL_MISSING: 30
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 8
  ANOMALY_BET_VOLUME_SPIKE: 5
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 41 | 10 | 12,300 | 7,950 | -4,350 | 0.646 |
| S01_NAKAANA1 | 33 | 9 | 6,600 | 4,040 | -2,560 | 0.612 |
| S02_TETSUBAN | 27 | 6 | 5,400 | 1,880 | -3,520 | 0.348 |

## 直近アラート (24h・新しい順)
```
[12:59:42] CIRCUIT_BREAKER_TRIP: {"cost": 12300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 41, "payout": 7950, "roi_7d": 0.646, "sid": "S00"}
[12:59:42] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 4.9, "baseline_n_days": 7, "baseline_stdev": 2.3, "hour": 12, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 14, "z_score": 3.91}
[12:56:49] CIRCUIT_BREAKER_TRIP: {"cost": 12000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 7950, "roi_7d": 0.662, "sid": "S00"}
[12:50:35] CIRCUIT_BREAKER_TRIP: {"cost": 5400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 27, "payout": 1880, "roi_7d": 0.348, "sid": "S02_TETSUBAN"}
[12:45:24] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1188}
[12:44:46] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1177}
[12:43:56] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1181}
[12:38:41] FINAL_MISSING: {"deadline": "2026-06-11T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061103031208", "sid": "S00"}
[12:37:21] CALIBRATION_DRIFT: {"avg_actual": 0.2371, "avg_pred": 0.4887, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 97, "overconf_pct": 51.5}
[12:35:33] CIRCUIT_BREAKER_TRIP: {"cost": 6600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 33, "payout": 4040, "roi_7d": 0.612, "sid": "S01_NAKAANA1"}
```

## 本日残レース: 86件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 58件 締切済
- 通知発射: scan=19 nid / final=19 nid / result=11 nid
- predictions: 14 / うち結果DB記録済: 12
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 035R | win | 1 | 0.5891 | 6.0 | 3.53 | 300 | scan=6.0 drift=+0.0% | 12:59:31 |
| S00 | 053R | win | 1 | 0.4111 | 9.4 | 3.86 | 300 | scan=15.8 drift=-40.5% | 12:29:22 |
| S00 | 239R | win | 1 | 0.4920 | 6.0 | 2.95 | 300 | scan=- drift=- | 12:23:32 |
| S02_TETSUBAN | 164R | win | 1 | 0.5891 | 2.2 | 1.30 | 200 | scan=2.2 drift=+0.0% | 12:18:31 |
| S01_NAKAANA1 | 094R | win | 1 | 0.5334 | 3.2 | 1.71 | 200 | scan=4.2 drift=-23.8% | 12:05:46 |
| S01_NAKAANA1 | 052R | win | 1 | 0.5123 | 3.2 | 1.64 | 200 | scan=- drift=- | 12:03:32 |
| S00 | 114R | win | 1 | 0.1543 | 5.6 | 0.86 | 300 | scan=5.6 drift=+0.0% | 11:52:32 |
| S00 | 093R | win | 1 | 0.2292 | 4.1 | 0.94 | 300 | scan=- drift=- | 11:33:20 |
| S01_NAKAANA1 | 051R | win | 1 | 0.5990 | 4.8 | 2.88 | 200 | scan=- drift=- | 11:30:25 |
| S00 | 051R | win | 1 | 0.5990 | 4.8 | 2.88 | 300 | scan=7.3 drift=-34.2% | 11:30:25 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 58 | +6.2% | -62.9% | +274.6% | 19 | 8 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 443.8s |
| **Latency** (scan→final max) | 616.2s |
| **Traffic** (notifications 24h) | 76 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,400円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 373 | 0.4697 | 0.2949 | +0.1748 | 🟡+37% | 0.2364 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 152 | 0.4199 | 0.2697 | 0.2170 | 🔴-0.10 | 0.801 |
| S01_NAKAANA1 | win | 140 | 0.4886 | 0.2857 | 0.2431 | 🔴-0.19 | 0.72 |
| S02_TETSUBAN | win | 81 | 0.5303 | 0.3580 | 0.2613 | 🔴-0.14 | 0.607 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1254 | 0.1667 | ✅-0.0412 |
| 0.15-0.20 | 5 | 0.1835 | 0.2000 | ✅-0.0165 |
| 0.20-0.30 | 6 | 0.2236 | 0.3333 | 🔴-0.1097 |
| 0.30-0.50 | 139 | 0.4202 | 0.2302 | 🔴+0.1900 |
| 0.50+ | 209 | 0.5421 | 0.3541 | 🔴+0.1880 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 36 | 0.735 |
| win | <5.0 | ✅learned | 69 | 0.717 |
| win | <10.0 | ✅learned | 43 | 0.508 |
| win | <20.0 | ✅learned | 14 | 0.21 |
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
_auto-generated by claude_snapshot.py at 2026-06-11T13:00:02.011133+09:00_