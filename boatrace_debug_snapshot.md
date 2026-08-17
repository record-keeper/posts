# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-17T16:30:01.859826+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×66 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×66 (24h)
- 🟡 FINAL_MISSING×64 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-08-17T16:20:40]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×48  [2026-08-17T16:06:28]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×72  [2026-08-17T16:06:28]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×24  [2026-08-17T16:06:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×43  [2026-08-17T15:42:05]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-17T15:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-17T15:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-17T15:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_DROP  ×11  [2026-08-17T13:00:18]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-17T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=71<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-17T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=171<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-17T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=37 hit%=21.6% ROI=0.64 (コスト 10,600/回収 6,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-17T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=9 pred=0.1189 actual=0.1111 gap=+0.0078`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-17T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=12 pred=0.1827 actual=0.0833 gap=+0.0994`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-17T06:00:14]
- key: `DRIFT_BUCKET|drift ≥+30%: n=40 hit%=22.5% ROI=0.91 (コスト 11,000/回収 9,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-08-17T06:00:14]
- key: `ROI_STAT|S00: n=171 hit%=22.8% hit_CI[Bonf]=[14.9,33.2]% ROI=0.63 ROI_boot95=[0.44,0.87]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-17T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=176 hit%=21.6% hit_CI[Bonf]=[14.0,31.7]% ROI=0.69 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-17T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-17T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=71 hit%=50.7% hit_CI[Bonf]=[34.4,66.8]% ROI=0.80 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-08-17T06:00:14]
- key: `ORPHAN_SCAN|208 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.74MB / last modified 2026-08-17T16:29:04.640864+09:00

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
e 15/4: boats=6 odds=190/191
2026-08-17 16:28:00,165 [INFO] predictor: CALIBRATION_MODE=on
2026-08-17 16:28:00,166 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-17 16:28:00,170 [INFO] run_cycle: fetched 15/4 [scan]: 156 combos
2026-08-17 16:28:00,281 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-17 16:28:03,386 [INFO] run_cycle: === run_cycle 16:28:03 ===
2026-08-17 16:28:03,386 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-17 16:28:03,386 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-17 16:28:03,416 [INFO] predictor: Models loaded OK
2026-08-17 16:28:14,474 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=02&hd=20260817: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-17 16:28:25,887 [INFO] scraper: odds3t: 120/120 parsed
2026-08-17 16:28:26,959 [INFO] scraper: odds3f: 20/20 parsed
2026-08-17 16:28:28,064 [INFO] scraper: odds2t: 30/30 parsed
2026-08-17 16:28:28,065 [INFO] scraper: odds2f: 15/15 parsed
2026-08-17 16:28:29,165 [INFO] scraper: odds_win: 6/6 parsed
2026-08-17 16:28:29,165 [INFO] scraper: fetch_race 02/12: boats=6 odds=191/191
2026-08-17 16:28:29,169 [INFO] predictor: CALIBRATION_MODE=on
2026-08-17 16:28:29,169 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-17 16:28:29,173 [INFO] run_cycle: fetched 02/12 [final]: 156 combos
2026-08-17 16:28:29,434 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-17 16:29:03,880 [INFO] run_cycle: === run_cycle 16:29:03 ===
2026-08-17 16:29:03,880 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-17 16:29:03,880 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-17 16:29:03,925 [INFO] predictor: Models loaded OK
2026-08-17 16:29:04,113 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 30, 'result': 15, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 120
  CIRCUIT_BREAKER_TRIP: 66
  FINAL_MISSING: 64
  CIRCUIT_BREAKER_NO_ACTION: 51
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 11
  ANOMALY_BET_VOLUME_DROP: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 43 | 9 | 12,900 | 6,180 | -6,720 | 0.479 |
| S01_NAKAANA1 | 49 | 11 | 9,800 | 7,180 | -2,620 | 0.733 |
| S02_TETSUBAN | 23 | 8 | 4,600 | 2,280 | -2,320 | 0.496 |

## 直近アラート (24h・新しい順)
```
[16:28:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1196}
[16:28:00] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1197}
[16:21:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1188}
[16:20:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1178}
[16:19:28] CIRCUIT_BREAKER_TRIP: {"cost": 4600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 23, "payout": 2280, "roi_7d": 0.496, "sid": "S02_TETSUBAN"}
[16:17:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1187}
[16:16:21] CIRCUIT_BREAKER_TRIP: {"cost": 4400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 22, "payout": 2280, "roi_7d": 0.518, "sid": "S02_TETSUBAN"}
[16:16:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1198}
[16:16:21] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.235, "baseline_mean": 0.72, "baseline_stdev": 0.096, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.955, "today_scan_count": 22, "z_score": 2.43}
[16:15:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1192}
```

## 本日残レース: 42件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 126件 締切済
- 通知発射: scan=22 nid / final=25 nid / result=12 nid
- predictions: 16 / うち結果DB記録済: 13
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 203R | win | 1 | 0.4989 | 2.0 | 1.00 | 200 | scan=- drift=- | 16:19:20 |
| S02_TETSUBAN | 1312R | win | 1 | 0.5990 | 2.3 | 1.38 | 200 | scan=2.2 drift=+4.5% | 16:16:19 |
| S01_NAKAANA1 | 228R | win | 1 | 0.5735 | 3.7 | 2.12 | 200 | scan=- drift=- | 15:57:20 |
| S02_TETSUBAN | 058R | win | 1 | 0.5253 | 2.4 | 1.26 | 200 | scan=- drift=- | 15:05:19 |
| S00 | 058R | win | 1 | 0.5253 | 18.5 | 9.72 | 300 | scan=42.0 drift=-56.0% | 15:04:19 |
| S02_TETSUBAN | 057R | win | 1 | 0.5663 | 2.4 | 1.36 | 200 | scan=- drift=- | 14:33:18 |
| S02_TETSUBAN | 139R | win | 1 | 0.5476 | 2.4 | 1.31 | 200 | scan=- drift=- | 14:30:20 |
| S01_NAKAANA1 | 178R | win | 1 | 0.3177 | 3.9 | 1.24 | 200 | scan=3.8 drift=+2.6% | 14:11:19 |
| S00 | 118R | win | 1 | 0.4092 | 7.5 | 3.07 | 300 | scan=8.2 drift=-8.5% | 14:04:18 |
| S00 | 177R | win | 1 | 0.2173 | 16.8 | 3.65 | 300 | scan=11.2 drift=+50.0% | 13:26:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 70 | +4.2% | -62.9% | +207.5% | 18 | 9 | 35 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 488.8s |
| **Latency** (scan→final max) | 602.3s |
| **Traffic** (notifications 24h) | 71 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,100円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 1,000円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 412 | 0.4651 | 0.2694 | +0.1957 | 🟡+42% | 0.2361 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 167 | 0.4147 | 0.2275 | 0.2182 | 🔴-0.24 | 0.635 |
| S01_NAKAANA1 | win | 173 | 0.4869 | 0.2197 | 0.2496 | 🔴-0.46 | 0.722 |
| S02_TETSUBAN | win | 72 | 0.5295 | 0.4861 | 0.2454 | ✅+0.02 | 0.753 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 9 | 0.1189 | 0.1111 | ✅+0.0078 |
| 0.15-0.20 | 12 | 0.1827 | 0.0833 | 🔴+0.0994 |
| 0.20-0.30 | 8 | 0.2246 | 0.3750 | 🔴-0.1504 |
| 0.30-0.50 | 157 | 0.4144 | 0.2293 | 🔴+0.1851 |
| 0.50+ | 224 | 0.5417 | 0.3125 | 🔴+0.2292 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 111 | 0.765 |
| win | <5.0 | ✅learned | 191 | 0.734 |
| win | <10.0 | ✅learned | 96 | 0.446 |
| win | <20.0 | ✅learned | 30 | 0.227 |
| win | <50.0 | ⚠️fallback | 7 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-08-17T16:30:01.859826+09:00_