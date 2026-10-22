# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-22T13:40:01.377190+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×58 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×4 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-22T13:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×24  [2026-10-22T13:15:01]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 STRATEGY_CI_FAIL  ×33  [2026-10-22T13:04:32]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CIRCUIT_BREAKER_TRIP  ×54  [2026-10-22T12:43:38]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×54  [2026-10-22T12:43:38]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×37  [2026-10-22T12:38:19]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-22T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=84<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-22T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=175<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-22T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=185<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-22T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1269 actual=0.3333 gap=-0.2064`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-22T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=33 pred=0.3210 actual=0.2121 gap=+0.1089`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-10-22T06:00:13]
- key: `ORPHAN_SCAN|151 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-22T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1833 actual=0.0000 gap=+0.1833`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-22T06:00:13]
- key: `ROI_STAT|S00: n=185 hit%=28.1% hit_CI[Bonf]=[19.7,38.4]% ROI=0.76 ROI_boot95=[0.55,0.98]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-22T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=175 hit%=36.0% hit_CI[Bonf]=[26.4,46.9]% ROI=0.98 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-22T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=84 hit%=52.4% hit_CI[Bonf]=[37.2,67.2]% ROI=0.96 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-22T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=29 hit%=44.8% ROI=1.16 (コスト 8,300/回収 9,630)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-22T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=47 hit%=34.0% ROI=0.72 (コスト 11,200/回収 8,120)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-22T06:00:13]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=92 hit%=42.4% ROI=1.19 (コスト 20,800/回収 24,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-22T06:00:13]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=63 hit%=33.3% ROI=0.86 (コスト 15,100/回収 13,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.42MB / last modified 2026-10-22T13:39:43.698950+09:00

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
29/30 parsed
2026-10-22 13:38:24,767 [INFO] scraper: odds2f: 15/15 parsed
2026-10-22 13:38:25,892 [INFO] scraper: odds_win: 6/6 parsed
2026-10-22 13:38:25,892 [INFO] scraper: fetch_race 18/11: boats=6 odds=190/191
2026-10-22 13:38:25,894 [INFO] predictor: CALIBRATION_MODE=on
2026-10-22 13:38:25,894 [INFO] predictor: combos: {'win': 6, '2t': 29, '3t': 120}
2026-10-22 13:38:25,899 [INFO] run_cycle: fetched 18/11 [scan]: 155 combos
2026-10-22 13:38:26,004 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-22 13:39:03,218 [INFO] run_cycle: === run_cycle 13:39:03 ===
2026-10-22 13:39:03,219 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-22 13:39:03,219 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-22 13:39:03,247 [INFO] predictor: Models loaded OK
2026-10-22 13:39:14,391 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=16&hd=20261022: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-22 13:39:25,518 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=16&hd=20261022: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-10-22 13:39:39,067 [INFO] scraper: odds3t: 120/120 parsed
2026-10-22 13:39:40,198 [INFO] scraper: odds3f: 20/20 parsed
2026-10-22 13:39:41,384 [INFO] scraper: odds2t: 29/30 parsed
2026-10-22 13:39:41,385 [INFO] scraper: odds2f: 13/15 parsed
2026-10-22 13:39:42,459 [INFO] scraper: odds_win: 4/6 parsed
2026-10-22 13:39:42,459 [INFO] scraper: fetch_race 16/7: boats=6 odds=186/191
2026-10-22 13:39:42,462 [INFO] predictor: CALIBRATION_MODE=on
2026-10-22 13:39:42,462 [INFO] predictor: combos: {'win': 4, '2t': 29, '3t': 120}
2026-10-22 13:39:42,466 [INFO] run_cycle: fetched 16/7 [scan]: 153 combos
2026-10-22 13:39:42,661 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 85
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 85
  }
]
```

## Phase別通知記録 (24h)
{'final': 31, 'result': 20, 'scan': 34}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 59
  FINAL_MISSING: 58
  ANOMALY_SCAN_FINAL_RATIO: 31
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 4
  CIRCUIT_BREAKER_NO_ACTION: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 44 | 12 | 13,200 | 8,400 | -4,800 | 0.636 |
| S01_NAKAANA1 | 46 | 15 | 9,200 | 7,180 | -2,020 | 0.78 |
| S02_TETSUBAN | 15 | 9 | 3,000 | 3,780 | +780 | 1.26 |

## 直近アラート (24h・新しい順)
```
[13:39:42] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1247}
[13:38:26] FINAL_MISSING: {"deadline": "2026-10-22T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102203031208", "sid": "S00"}
[13:38:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1255}
[13:36:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1264}
[13:35:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1254}
[13:34:51] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1246}
[13:33:18] FINAL_MISSING: {"deadline": "2026-10-22T09:01:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102214020901", "sid": "S00"}
[13:33:18] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1265}
[13:32:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1284}
[13:31:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1315}
```

## 本日残レース: 85件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 83件 締切済
- 通知発射: scan=18 nid / final=16 nid / result=9 nid
- predictions: 12 / うち結果DB記録済: 10
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 178R | win | 1 | 0.5174 | 4.2 | 2.17 | 200 | scan=3.3 drift=+27.3% | 13:29:20 |
| S00 | 046R | win | 1 | 0.1760 | 4.7 | 0.83 | 300 | scan=5.2 drift=-9.6% | 13:11:19 |
| S01_NAKAANA1 | 136R | win | 1 | 0.5123 | 4.2 | 2.15 | 200 | scan=- drift=- | 12:59:30 |
| S01_NAKAANA1 | 056R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=- drift=- | 12:53:30 |
| S00 | 056R | win | 1 | 0.4111 | 8.2 | 3.37 | 300 | scan=17.2 drift=-52.3% | 12:52:19 |
| S00 | 055R | win | 1 | 0.3177 | 15.0 | 4.77 | 300 | scan=12.7 drift=+18.1% | 12:26:30 |
| S01_NAKAANA1 | 164R | win | 1 | 0.2290 | 3.1 | 0.71 | 200 | scan=- drift=- | 12:20:20 |
| S01_NAKAANA1 | 064R | win | 1 | 0.5476 | 3.5 | 1.92 | 200 | scan=3.5 drift=+0.0% | 12:17:20 |
| S02_TETSUBAN | 115R | win | 1 | 0.5334 | 2.0 | 1.07 | 200 | scan=2.0 drift=+0.0% | 12:09:19 |
| S01_NAKAANA1 | 147R | win | 1 | 0.4111 | 3.9 | 1.60 | 200 | scan=3.2 drift=+21.9% | 11:21:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 63 | +28.2% | -52.3% | +495.8% | 10 | 4 | 42 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 448.4s |
| **Latency** (scan→final max) | 650.9s |
| **Traffic** (notifications 24h) | 85 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 1,600円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 448 | 0.4798 | 0.3549 | +0.1249 | 🟡+26% | 0.2433 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 186 | 0.4421 | 0.2796 | 0.2373 | 🔴-0.18 | 0.753 |
| S01_NAKAANA1 | win | 178 | 0.4935 | 0.3596 | 0.2431 | 🔴-0.06 | 0.971 |
| S02_TETSUBAN | win | 84 | 0.5345 | 0.5119 | 0.2573 | 🔴-0.03 | 0.935 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1269 | 0.3333 | 🔴-0.2064 |
| 0.15-0.20 | 7 | 0.1833 | 0.0000 | 🔴+0.1833 |
| 0.20-0.30 | 8 | 0.2288 | 0.2500 | ✅-0.0212 |
| 0.30-0.50 | 157 | 0.4160 | 0.3248 | 🔴+0.0912 |
| 0.50+ | 268 | 0.5435 | 0.3843 | 🔴+0.1591 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 191 | 0.782 |
| win | <5.0 | ✅learned | 343 | 0.746 |
| win | <10.0 | ✅learned | 150 | 0.457 |
| win | <20.0 | ✅learned | 42 | 0.244 |
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
_auto-generated by claude_snapshot.py at 2026-10-22T13:40:01.377190+09:00_