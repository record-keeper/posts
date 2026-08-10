# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-10T13:30:04.294448+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×45 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×126 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×45 (24h)
- 🔴 PSI_DRIFT_DETECTED×35 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×9  [2026-08-10T13:20:23]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×25  [2026-08-10T13:04:34]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×50  [2026-08-10T13:04:34]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×25  [2026-08-10T13:04:34]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-10T13:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-10T13:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×36  [2026-08-10T12:34:18]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×38  [2026-08-10T11:02:54]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 ANOMALY_BET_VOLUME_DROP  ×50  [2026-08-10T10:00:07]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ORPHAN_SCAN  ×1  [2026-08-10T06:00:14]
- key: `ORPHAN_SCAN|173 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-10T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=20.0% ROI=0.61 (コスト 10,300/回収 6,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-10T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2237 actual=0.3636 gap=-0.1399`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-10T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=175<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-10T06:00:14]
- key: `ROI_STAT|S00: n=175 hit%=25.1% hit_CI[Bonf]=[17.0,35.6]% ROI=0.73 ROI_boot95=[0.51,0.96]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-10T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=167 hit%=24.0% hit_CI[Bonf]=[15.8,34.6]% ROI=0.71 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-10T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-10T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=66 hit%=50.0% hit_CI[Bonf]=[33.3,66.7]% ROI=0.93 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-10T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=66<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-10T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=38 hit%=34.2% ROI=0.83 (コスト 9,400/回収 7,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-10T06:00:14]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=67 hit%=28.4% ROI=0.80 (コスト 15,900/回収 12,650)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.01MB / last modified 2026-08-10T13:29:30.821825+09:00

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
er: odds_win: 5/6 parsed
2026-08-10 13:28:36,763 [INFO] scraper: fetch_race 18/7: boats=6 odds=190/191
2026-08-10 13:28:36,766 [INFO] predictor: CALIBRATION_MODE=on
2026-08-10 13:28:36,766 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-10 13:28:36,770 [INFO] run_cycle: fetched 18/7 [scan]: 155 combos
2026-08-10 13:28:36,888 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-10 13:29:03,659 [INFO] run_cycle: === run_cycle 13:29:03 ===
2026-08-10 13:29:03,659 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-10 13:29:03,659 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-10 13:29:03,689 [INFO] predictor: Models loaded OK
2026-08-10 13:29:14,742 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=11&jcd=21&hd=20260810: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-10 13:29:27,047 [INFO] scraper: odds3t: 120/120 parsed
2026-08-10 13:29:28,121 [INFO] scraper: odds3f: 20/20 parsed
2026-08-10 13:29:29,190 [INFO] scraper: odds2t: 30/30 parsed
2026-08-10 13:29:29,191 [INFO] scraper: odds2f: 15/15 parsed
2026-08-10 13:29:30,297 [INFO] scraper: odds_win: 4/6 parsed
2026-08-10 13:29:30,298 [INFO] scraper: fetch_race 21/11: boats=6 odds=189/191
2026-08-10 13:29:30,301 [INFO] predictor: CALIBRATION_MODE=on
2026-08-10 13:29:30,301 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-08-10 13:29:30,305 [INFO] run_cycle: fetched 21/11 [final]: 154 combos
2026-08-10 13:29:30,585 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-10 13:30:04,713 [INFO] run_cycle: === run_cycle 13:30:04 ===
2026-08-10 13:30:04,714 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-10 13:30:04,714 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-10 13:30:04,758 [INFO] predictor: Models loaded OK

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
    "c": 92
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 92
  }
]
```

## Phase別通知記録 (24h)
{'final': 35, 'result': 23, 'scan': 34}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 135
  FINAL_MISSING: 126
  CIRCUIT_BREAKER_TRIP: 45
  PSI_DRIFT_DETECTED: 35
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_BET_VOLUME_SPIKE: 19
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 12
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 8 | 10,500 | 7,980 | -2,520 | 0.76 |
| S01_NAKAANA1 | 45 | 9 | 9,000 | 5,200 | -3,800 | 0.578 |
| S02_TETSUBAN | 12 | 7 | 2,400 | 2,360 | -40 | 0.983 |

## 直近アラート (24h・新しい順)
```
[13:29:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1142}
[13:28:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1160}
[13:27:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1162}
[13:25:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1171}
[13:24:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1178}
[13:23:39] FINAL_MISSING: {"deadline": "2026-08-10T12:53:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081013061253", "sid": "S00"}
[13:23:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1169}
[13:23:39] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.162, "baseline_mean": 0.809, "baseline_stdev": 0.049, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.647, "today_scan_count": 17, "z_score": -3.28}
[13:22:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1179}
[13:21:33] CIRCUIT_BREAKER_TRIP: {"cost": 9000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 45, "payout": 5200, "roi_7d": 0.578, "sid": "S01_NAKAANA1"}
```

## 本日残レース: 84件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 72件 締切済
- 通知発射: scan=17 nid / final=13 nid / result=7 nid
- predictions: 9 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 239R | win | 1 | 0.4111 | 22.1 | 9.09 | 300 | scan=5.7 drift=+287.7% | 12:44:20 |
| S01_NAKAANA1 | 053R | win | 1 | 0.4988 | 3.6 | 1.80 | 200 | scan=- drift=- | 12:31:20 |
| S01_NAKAANA1 | 134R | win | 1 | 0.4111 | 4.3 | 1.77 | 200 | scan=4.5 drift=-4.4% | 11:51:19 |
| S00 | 237R | win | 1 | 0.4111 | 4.1 | 1.69 | 300 | scan=- drift=- | 11:43:18 |
| S01_NAKAANA1 | 237R | win | 1 | 0.4111 | 3.9 | 1.60 | 200 | scan=3.3 drift=+18.2% | 11:42:19 |
| S00 | 236R | win | 1 | 0.4920 | 5.6 | 2.76 | 300 | scan=5.2 drift=+7.7% | 11:09:30 |
| S00 | 082R | win | 1 | 0.5334 | 8.6 | 4.59 | 300 | scan=4.5 drift=+91.1% | 11:02:44 |
| S01_NAKAANA1 | 161R | win | 1 | 0.5891 | 4.1 | 2.42 | 200 | scan=- drift=- | 10:50:37 |
| S00 | 161R | win | 1 | 0.5891 | 4.1 | 2.42 | 300 | scan=- drift=- | 10:50:32 |
| S02_TETSUBAN | 206R | win | 1 | 0.5334 | 2.2 | 1.17 | 200 | scan=2.2 drift=+0.0% | 17:48:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 57 | +5.4% | -73.3% | +287.7% | 18 | 8 | 38 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 486.4s |
| **Latency** (scan→final max) | 653.2s |
| **Traffic** (notifications 24h) | 92 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 406 | 0.4627 | 0.2808 | +0.1819 | 🟡+39% | 0.2377 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 174 | 0.4164 | 0.2414 | 0.2286 | 🔴-0.25 | 0.723 |
| S01_NAKAANA1 | win | 167 | 0.4840 | 0.2395 | 0.2443 | 🔴-0.34 | 0.729 |
| S02_TETSUBAN | win | 65 | 0.5319 | 0.4923 | 0.2451 | ✅+0.02 | 0.863 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 11 | 0.1216 | 0.1818 | 🔴-0.0602 |
| 0.15-0.20 | 11 | 0.1835 | 0.1818 | ✅+0.0017 |
| 0.20-0.30 | 10 | 0.2236 | 0.4000 | 🔴-0.1764 |
| 0.30-0.50 | 159 | 0.4175 | 0.2201 | 🔴+0.1973 |
| 0.50+ | 213 | 0.5432 | 0.3333 | 🔴+0.2098 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 101 | 0.783 |
| win | <5.0 | ✅learned | 178 | 0.727 |
| win | <10.0 | ✅learned | 90 | 0.453 |
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
_auto-generated by claude_snapshot.py at 2026-08-10T13:30:04.294448+09:00_