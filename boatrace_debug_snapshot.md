# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-29T13:00:01.551955+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×22 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×39 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-29T12:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-29T12:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×58  [2026-07-29T12:02:18]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×116  [2026-07-29T12:02:18]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×58  [2026-07-29T12:02:18]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×11  [2026-07-29T12:00:43]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×54  [2026-07-29T11:58:30]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×61  [2026-07-29T11:56:40]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-29T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=82<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-29T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=178<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-29T06:00:10]
- key: `ORPHAN_SCAN|173 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-29T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=162<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-29T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=7 pred=0.1262 actual=0.1429 gap=-0.0167`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-29T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1785 actual=0.3750 gap=-0.1965`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-29T06:00:10]
- key: `ROI_STAT|S00: n=178 hit%=25.8% hit_CI[Bonf]=[17.6,36.2]% ROI=0.69 ROI_boot95=[0.49,0.92]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-29T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=162 hit%=27.2% hit_CI[Bonf]=[18.4,38.2]% ROI=0.77 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-29T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=82 hit%=50.0% hit_CI[Bonf]=[34.8,65.2]% ROI=0.98 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-29T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=29 hit%=24.1% ROI=0.41 (コスト 8,500/回収 3,480)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-29T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=44 hit%=34.1% ROI=0.91 (コスト 10,700/回収 9,710)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-29T06:00:10]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=74 hit%=32.4% ROI=0.76 (コスト 17,100/回収 13,030)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 8.94MB / last modified 2026-07-29T13:00:03.821705+09:00

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
[INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-29 12:58:04,297 [INFO] predictor: Models loaded OK
2026-07-29 12:58:15,423 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=09&hd=20260729: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-07-29 12:58:26,456 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=09&hd=20260729: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-07-29 12:58:38,674 [WARNING] scraper: beforeinfo parse failed: jcd=09 rno=6
2026-07-29 12:58:38,674 [WARNING] run_cycle: fetch None: 09/6
2026-07-29 12:58:38,675 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-29 12:59:04,073 [INFO] run_cycle: === run_cycle 12:59:04 ===
2026-07-29 12:59:04,073 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-29 12:59:04,073 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-29 12:59:04,106 [INFO] predictor: Models loaded OK
2026-07-29 12:59:15,443 [INFO] scraper: odds3t: 120/120 parsed
2026-07-29 12:59:16,558 [INFO] scraper: odds3f: 20/20 parsed
2026-07-29 12:59:17,633 [INFO] scraper: odds2t: 30/30 parsed
2026-07-29 12:59:17,634 [INFO] scraper: odds2f: 15/15 parsed
2026-07-29 12:59:18,709 [INFO] scraper: odds_win: 6/6 parsed
2026-07-29 12:59:18,709 [INFO] scraper: fetch_race 17/5: boats=6 odds=191/191
2026-07-29 12:59:18,712 [INFO] predictor: CALIBRATION_MODE=on
2026-07-29 12:59:18,712 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-29 12:59:18,717 [INFO] run_cycle: fetched 17/5 [final]: 156 combos
2026-07-29 12:59:21,106 [WARNING] scraper: beforeinfo parse failed: jcd=09 rno=6
2026-07-29 12:59:21,107 [WARNING] run_cycle: fetch None: 09/6
2026-07-29 12:59:21,107 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 56
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 56
  }
]
```

## Phase別通知記録 (24h)
{'final': 21, 'result': 14, 'scan': 21}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 138
  FINAL_MISSING: 39
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 22
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 11
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 8 | 12,600 | 5,550 | -7,050 | 0.44 |
| S01_NAKAANA1 | 33 | 9 | 6,600 | 4,900 | -1,700 | 0.742 |
| S02_TETSUBAN | 18 | 10 | 3,600 | 3,300 | -300 | 0.917 |

## 直近アラート (24h・新しい順)
```
[12:56:14] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1148}
[12:55:40] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1144}
[12:54:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1134}
[12:52:29] CIRCUIT_BREAKER_TRIP: {"cost": 12600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 42, "payout": 5550, "roi_7d": 0.44, "sid": "S00"}
[12:52:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1122}
[12:50:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1121}
[12:50:29] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.192, "baseline_mean": 0.747, "baseline_stdev": 0.085, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.556, "today_scan_count": 9, "z_score": -2.27}
[12:48:28] CIRCUIT_BREAKER_TRIP: {"cost": 12300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 41, "payout": 5550, "roi_7d": 0.451, "sid": "S00"}
[12:48:28] FINAL_MISSING: {"deadline": "2026-07-29T10:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072910051016", "sid": "S00"}
[12:48:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1109}
```

## 本日残レース: 105件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 51件 締切済
- 通知発射: scan=9 nid / final=8 nid / result=2 nid
- predictions: 5 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 222R | win | 1 | 0.3177 | 18.0 | 5.72 | 300 | scan=6.0 drift=+200.0% | 12:52:18 |
| S01_NAKAANA1 | 043R | win | 1 | 0.3177 | 3.9 | 1.24 | 200 | scan=3.2 drift=+21.9% | 12:50:20 |
| S00 | 163R | win | 1 | 0.1371 | 7.5 | 1.03 | 300 | scan=4.5 drift=+66.7% | 12:48:19 |
| S01_NAKAANA1 | 239R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 12:18:29 |
| S00 | 109R | win | 1 | 0.4111 | 19.5 | 8.02 | 300 | scan=4.1 drift=+375.6% | 12:11:19 |
| S01_NAKAANA1 | 156R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=3.9 drift=-10.3% | 17:46:19 |
| S01_NAKAANA1 | 0410R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=3.8 drift=+15.8% | 16:39:18 |
| S00 | 192R | win | 1 | 0.5174 | 12.0 | 6.21 | 300 | scan=10.5 drift=+14.3% | 16:04:18 |
| S01_NAKAANA1 | 152R | win | 1 | 0.5476 | 4.6 | 2.52 | 200 | scan=- drift=- | 15:49:19 |
| S02_TETSUBAN | 0310R | win | 1 | 0.3177 | 2.5 | 0.79 | 200 | scan=2.9 drift=-13.8% | 15:19:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 47 | +18.2% | -86.1% | +375.6% | 13 | 8 | 34 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 491.8s |
| **Latency** (scan→final max) | 594.5s |
| **Traffic** (notifications 24h) | 56 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 415 | 0.4627 | 0.3060 | +0.1567 | 🟡+34% | 0.2327 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 176 | 0.4209 | 0.2557 | 0.2215 | 🔴-0.16 | 0.68 |
| S01_NAKAANA1 | win | 158 | 0.4737 | 0.2595 | 0.2367 | 🔴-0.23 | 0.734 |
| S02_TETSUBAN | win | 81 | 0.5321 | 0.5062 | 0.2493 | 🔴+0.00 | 0.989 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 7 | 0.1262 | 0.1429 | ✅-0.0167 |
| 0.15-0.20 | 8 | 0.1785 | 0.3750 | 🔴-0.1965 |
| 0.20-0.30 | 12 | 0.2272 | 0.2500 | ✅-0.0228 |
| 0.30-0.50 | 166 | 0.4147 | 0.2530 | 🔴+0.1617 |
| 0.50+ | 218 | 0.5403 | 0.3578 | 🔴+0.1825 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 89 | 0.799 |
| win | <5.0 | ✅learned | 159 | 0.723 |
| win | <10.0 | ✅learned | 82 | 0.455 |
| win | <20.0 | ✅learned | 26 | 0.216 |
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
_auto-generated by claude_snapshot.py at 2026-07-29T13:00:01.551955+09:00_