# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-13T16:00:01.560870+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×19 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×76 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×19 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-13T15:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×5  [2026-07-13T15:08:26]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×57  [2026-07-13T15:03:26]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×57  [2026-07-13T15:03:26]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-07-13T14:30:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 CIRCUIT_BREAKER_TRIP  ×18  [2026-07-13T13:02:27]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×7  [2026-07-13T12:27:26]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×45  [2026-07-13T12:00:05]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-13T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=153<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-13T06:00:06]
- key: `ROI_STAT|S00: n=178 hit%=30.3% hit_CI[Bonf]=[21.5,41.0]% ROI=0.79 ROI_boot95=[0.60,1.01]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-13T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S00: n=178<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-13T06:00:06]
- key: `ROI_STAT|S01_NAKAANA1: n=153 hit%=30.1% hit_CI[Bonf]=[20.6,41.6]% ROI=0.80 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-13T06:00:06]
- key: `ROI_STAT|S02_TETSUBAN: n=68 hit%=45.6% hit_CI[Bonf]=[29.6,62.5]% ROI=0.90 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-13T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=68<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-13T06:00:06]
- key: `ORPHAN_SCAN|172 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-13T06:00:06]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=32.4% ROI=0.84 (コスト 9,900/回収 8,340)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-13T06:00:06]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=47 hit%=31.9% ROI=0.75 (コスト 11,500/回収 8,580)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-13T06:00:06]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=86 hit%=34.9% ROI=0.99 (コスト 19,900/回収 19,730)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-13T06:00:06]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=36 hit%=33.3% ROI=0.77 (コスト 8,800/回収 6,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-13T06:00:06]
- key: `DRIFT_BUCKET|drift ≥+30%: n=30 hit%=20.0% ROI=0.39 (コスト 8,400/回収 3,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 7.66MB / last modified 2026-07-13T16:00:04.454684+09:00

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
5000
2026-07-13 15:58:03,473 [INFO] predictor: Models loaded OK
2026-07-13 15:58:14,646 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=9&jcd=04&hd=20260713: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-07-13 15:58:27,130 [INFO] scraper: odds3t: 120/120 parsed
2026-07-13 15:58:28,253 [INFO] scraper: odds3f: 20/20 parsed
2026-07-13 15:58:29,381 [INFO] scraper: odds2t: 30/30 parsed
2026-07-13 15:58:29,383 [INFO] scraper: odds2f: 15/15 parsed
2026-07-13 15:58:30,497 [INFO] scraper: odds_win: 2/6 parsed
2026-07-13 15:58:30,497 [INFO] scraper: fetch_race 04/9: boats=6 odds=187/191
2026-07-13 15:58:30,501 [INFO] predictor: CALIBRATION_MODE=on
2026-07-13 15:58:30,501 [INFO] predictor: combos: {'win': 2, '2t': 30, '3t': 120}
2026-07-13 15:58:30,506 [INFO] run_cycle: fetched 04/9 [scan]: 152 combos
2026-07-13 15:58:30,705 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-13 15:59:03,719 [INFO] run_cycle: === run_cycle 15:59:03 ===
2026-07-13 15:59:03,719 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-13 15:59:03,719 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-13 15:59:03,762 [INFO] predictor: Models loaded OK
2026-07-13 15:59:16,319 [INFO] scraper: odds3t: 120/120 parsed
2026-07-13 15:59:17,428 [INFO] scraper: odds3f: 20/20 parsed
2026-07-13 15:59:18,613 [INFO] scraper: odds2t: 30/30 parsed
2026-07-13 15:59:18,614 [INFO] scraper: odds2f: 15/15 parsed
2026-07-13 15:59:19,696 [INFO] scraper: odds_win: 2/6 parsed
2026-07-13 15:59:19,696 [INFO] scraper: fetch_race 05/10: boats=6 odds=187/191
2026-07-13 15:59:19,700 [INFO] predictor: CALIBRATION_MODE=on
2026-07-13 15:59:19,700 [INFO] predictor: combos: {'win': 2, '2t': 30, '3t': 120}
2026-07-13 15:59:19,705 [INFO] run_cycle: fetched 05/10 [scan]: 152 combos
2026-07-13 15:59:19,815 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 22, 'result': 8, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 158
  FINAL_MISSING: 76
  CIRCUIT_BREAKER_NO_ACTION: 25
  CIRCUIT_BREAKER_TRIP: 19
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 8
  ANOMALY_BET_VOLUME_DROP: 4
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 47 | 18 | 14,100 | 14,700 | +600 | 1.043 |
| S01_NAKAANA1 | 38 | 12 | 7,600 | 5,980 | -1,620 | 0.787 |
| S02_TETSUBAN | 18 | 8 | 3,600 | 3,860 | +260 | 1.072 |

## 直近アラート (24h・新しい順)
```
[15:59:19] FINAL_MISSING: {"deadline": "2026-07-13T09:24:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071323030924", "sid": "S00"}
[15:29:33] FINAL_MISSING: {"deadline": "2026-07-13T11:57:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071314081157", "sid": "S00"}
[15:27:20] FINAL_MISSING: {"deadline": "2026-07-13T13:56:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071303071356", "sid": "S00"}
[15:25:19] FINAL_MISSING: {"deadline": "2026-07-13T12:54:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071304031254", "sid": "S00"}
[15:12:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1044}
[15:11:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1031}
[15:10:52] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1023}
[15:09:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1043}
[15:08:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1042}
[15:07:43] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1032}
```

## 本日残レース: 53件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 103件 締切済
- 通知発射: scan=15 nid / final=15 nid / result=6 nid
- predictions: 7 / うち結果DB記録済: 6
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 7件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 072R | win | 1 | 0.5735 | 2.1 | 1.20 | 200 | scan=- drift=- | 15:44:29 |
| S01_NAKAANA1 | 0310R | win | 1 | 0.5334 | 3.1 | 1.65 | 200 | scan=3.0 drift=+3.3% | 15:19:18 |
| S00 | 226R | win | 1 | 0.1760 | 4.9 | 0.86 | 300 | scan=- drift=- | 14:45:42 |
| S01_NAKAANA1 | 043R | win | 1 | 0.2307 | 4.5 | 1.04 | 200 | scan=4.6 drift=-2.2% | 12:51:19 |
| S01_NAKAANA1 | 2310R | win | 1 | 0.5174 | 4.8 | 2.48 | 200 | scan=3.3 drift=+45.5% | 12:49:30 |
| S02_TETSUBAN | 163R | win | 1 | 0.5891 | 2.2 | 1.30 | 200 | scan=- drift=- | 12:47:19 |
| S01_NAKAANA1 | 149R | win | 1 | 0.3177 | 3.5 | 1.11 | 200 | scan=- drift=- | 12:25:20 |
| S02_TETSUBAN | 205R | win | 1 | 0.5174 | 2.1 | 1.09 | 200 | scan=- drift=- | 17:34:29 |
| S00 | 153R | win | 1 | 0.1760 | 7.5 | 1.32 | 300 | scan=7.5 drift=+0.0% | 16:20:30 |
| S00 | 227R | win | 1 | 0.3177 | 9.9 | 3.15 | 300 | scan=13.1 drift=-24.4% | 15:16:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 56 | +20.7% | -73.3% | +533.3% | 15 | 5 | 37 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 468.8s |
| **Latency** (scan→final max) | 610.6s |
| **Traffic** (notifications 24h) | 56 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 397 | 0.4711 | 0.3275 | +0.1437 | 🟡+30% | 0.2366 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 175 | 0.4338 | 0.2971 | 0.2260 | 🔴-0.08 | 0.768 |
| S01_NAKAANA1 | win | 155 | 0.4823 | 0.3097 | 0.2384 | 🔴-0.12 | 0.815 |
| S02_TETSUBAN | win | 67 | 0.5427 | 0.4478 | 0.2602 | 🔴-0.05 | 0.887 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1777 | 0.5714 | 🔴-0.3938 |
| 0.20-0.30 | 16 | 0.2282 | 0.1875 | ✅+0.0407 |
| 0.30-0.50 | 144 | 0.4180 | 0.2917 | 🔴+0.1263 |
| 0.50+ | 224 | 0.5418 | 0.3616 | 🔴+0.1802 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 70 | 0.794 |
| win | <5.0 | ✅learned | 138 | 0.704 |
| win | <10.0 | ✅learned | 73 | 0.471 |
| win | <20.0 | ✅learned | 23 | 0.225 |
| win | <50.0 | ⚠️fallback | 3 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-07-13T16:00:01.560870+09:00_