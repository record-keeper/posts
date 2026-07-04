# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-04T12:40:01.613230+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×11 (24h)
- 🔴 PSI_DRIFT_DETECTED×10 (24h)
- 🟡 FINAL_MISSING×8 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×2  [2026-07-04T12:35:21]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×74  [2026-07-04T12:02:45]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×37  [2026-07-04T12:02:45]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-04T12:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-04T12:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×30  [2026-07-04T09:56:09]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=168<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=77<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-04T06:00:14]
- key: `ORPHAN_SCAN|154 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=137<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-04T06:00:14]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=25 hit%=32.0% ROI=1.06 (コスト 6,100/回収 6,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-04T06:00:14]
- key: `DRIFT_BUCKET|drift ≥+30%: n=30 hit%=23.3% ROI=0.51 (コスト 8,400/回収 4,310)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=22 pred=0.3216 actual=0.1818 gap=+0.1397`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-04T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=36 hit%=27.8% ROI=0.85 (コスト 10,500/回収 8,940)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-07-04T06:00:14]
- key: `ROI_STAT|S00: n=168 hit%=26.8% hit_CI[Bonf]=[18.2,37.6]% ROI=0.72 ROI_boot95=[0.53,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-04T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=137 hit%=31.4% hit_CI[Bonf]=[21.3,43.6]% ROI=0.85 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-04T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=77 hit%=32.5% hit_CI[Bonf]=[19.4,48.9]% ROI=0.54 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-04T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=41 hit%=24.4% ROI=0.61 (コスト 9,700/回収 5,900)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-04T06:00:14]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=91 hit%=29.7% ROI=0.71 (コスト 21,300/回収 15,180)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-04T06:00:14]
- key: `CALIBRATION_LIVE|bt=win: n=382 pred=0.4791 actual=0.2958 error=+0.1833 (+38%) brier=0.2396 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.69MB / last modified 2026-07-04T12:39:23.173033+09:00

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
 in 1s
2026-07-04 12:38:28,457 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=2&jcd=22&hd=20260704: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-07-04 12:38:41,516 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=2&jcd=22&hd=20260704: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-07-04 12:38:41,516 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/racelist?rno=2&jcd=22&hd=20260704
2026-07-04 12:38:41,516 [ERROR] scraper: racelist fetch failed: jcd=22 rno=2
2026-07-04 12:38:41,516 [WARNING] run_cycle: fetch None: 22/2
2026-07-04 12:38:41,783 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-04 12:39:05,619 [INFO] run_cycle: === run_cycle 12:39:05 ===
2026-07-04 12:39:05,619 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-04 12:39:05,619 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-04 12:39:05,665 [INFO] predictor: Models loaded OK
2026-07-04 12:39:17,204 [INFO] scraper: odds3t: 120/120 parsed
2026-07-04 12:39:18,364 [INFO] scraper: odds3f: 20/20 parsed
2026-07-04 12:39:19,516 [INFO] scraper: odds2t: 30/30 parsed
2026-07-04 12:39:19,517 [INFO] scraper: odds2f: 13/15 parsed
2026-07-04 12:39:20,661 [INFO] scraper: odds_win: 2/6 parsed
2026-07-04 12:39:20,661 [INFO] scraper: fetch_race 21/10: boats=6 odds=185/191
2026-07-04 12:39:20,674 [INFO] predictor: CALIBRATION_MODE=on
2026-07-04 12:39:20,674 [INFO] predictor: combos: {'win': 2, '2t': 30, '3t': 120}
2026-07-04 12:39:20,682 [INFO] run_cycle: fetched 21/10 [scan]: 152 combos
2026-07-04 12:39:23,131 [WARNING] scraper: beforeinfo parse failed: jcd=06 rno=4
2026-07-04 12:39:23,131 [WARNING] run_cycle: fetch None: 06/4
2026-07-04 12:39:23,131 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 71
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 71
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 17, 'scan': 25}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 82
  CIRCUIT_BREAKER_NO_ACTION: 32
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 11
  CIRCUIT_BREAKER_TRIP: 11
  PSI_DRIFT_DETECTED: 10
  FINAL_MISSING: 8
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 39 | 12 | 11,700 | 9,120 | -2,580 | 0.779 |
| S01_NAKAANA1 | 34 | 13 | 6,800 | 6,320 | -480 | 0.929 |
| S02_TETSUBAN | 21 | 9 | 4,200 | 3,040 | -1,160 | 0.724 |

## 直近アラート (24h・新しい順)
```
[12:39:23] FINAL_MISSING: {"deadline": "2026-07-04T12:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070409041209", "sid": "S00"}
[12:27:40] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.201, "baseline_mean": 0.837, "baseline_stdev": 0.103, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.636, "today_scan_count": 11, "z_score": -1.95}
[12:18:29] FINAL_MISSING: {"deadline": "2026-07-04T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070421061047", "sid": "S00"}
[12:02:45] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:02:45] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[12:02:45] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[11:59:27] FINAL_MISSING: {"deadline": "2026-07-04T11:29:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070413031129", "sid": "S01_NAKAANA1"}
[11:56:36] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.237, "baseline_mean": 0.837, "baseline_stdev": 0.103, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.6, "today_scan_count": 10, "z_score": -2.3}
[11:50:40] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.282, "baseline_mean": 0.837, "baseline_stdev": 0.103, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.556, "today_scan_count": 9, "z_score": -2.73}
[11:49:40] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.212, "baseline_mean": 0.837, "baseline_stdev": 0.103, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.625, "today_scan_count": 8, "z_score": -2.06}
```

## 本日残レース: 116件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 52件 締切済
- 通知発射: scan=11 nid / final=9 nid / result=5 nid
- predictions: 6 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 222R | win | 1 | 0.5050 | 4.2 | 2.12 | 300 | scan=5.2 drift=-19.2% | 12:37:33 |
| S01_NAKAANA1 | 188R | win | 1 | 0.5123 | 3.1 | 1.59 | 200 | scan=4.2 drift=-26.2% | 12:00:26 |
| S00 | 218R | win | 1 | 0.5123 | 8.8 | 4.51 | 300 | scan=6.7 drift=+31.3% | 11:46:44 |
| S01_NAKAANA1 | 237R | win | 1 | 0.4111 | 4.6 | 1.89 | 200 | scan=4.6 drift=+0.0% | 11:19:31 |
| S00 | 183R | win | 1 | 0.5123 | 5.0 | 2.56 | 300 | scan=- drift=- | 09:35:33 |
| S00 | 233R | win | 1 | 0.5334 | 5.2 | 2.77 | 300 | scan=4.5 drift=+15.6% | 09:28:21 |
| S02_TETSUBAN | 204R | win | 1 | 0.6037 | 2.2 | 1.33 | 200 | scan=- drift=- | 19:00:26 |
| S00 | 197R | win | 1 | 0.2173 | 8.2 | 1.78 | 300 | scan=8.2 drift=+0.0% | 18:18:22 |
| S00 | 194R | win | 1 | 0.1720 | 6.0 | 1.03 | 300 | scan=- drift=- | 17:03:22 |
| S01_NAKAANA1 | 124R | win | 1 | 0.4111 | 4.1 | 1.69 | 200 | scan=- drift=- | 16:58:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 62 | +9.8% | -68.9% | +584.6% | 21 | 8 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 417.8s |
| **Latency** (scan→final max) | 608.4s |
| **Traffic** (notifications 24h) | 71 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 383 | 0.4799 | 0.3029 | +0.1770 | 🟡+37% | 0.2403 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 168 | 0.4429 | 0.2798 | 0.2245 | 🔴-0.11 | 0.74 |
| S01_NAKAANA1 | win | 139 | 0.4912 | 0.3165 | 0.2440 | 🔴-0.13 | 0.854 |
| S02_TETSUBAN | win | 76 | 0.5409 | 0.3289 | 0.2683 | 🔴-0.22 | 0.547 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1746 | 0.4286 | 🔴-0.2540 |
| 0.20-0.30 | 14 | 0.2291 | 0.0714 | 🔴+0.1577 |
| 0.30-0.50 | 133 | 0.4226 | 0.2707 | 🔴+0.1519 |
| 0.50+ | 226 | 0.5437 | 0.3363 | 🔴+0.2074 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 55 | 0.737 |
| win | <5.0 | ✅learned | 113 | 0.716 |
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
_auto-generated by claude_snapshot.py at 2026-07-04T12:40:01.613230+09:00_