# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-03T13:50:01.557064+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×38 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×10 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×47  [2026-07-03T13:03:29]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×47  [2026-07-03T13:03:29]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CIRCUIT_BREAKER_TRIP  ×59  [2026-07-03T12:51:23]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-03T12:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×1  [2026-07-03T11:35:30]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-03T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=74<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-03T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=137<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-03T06:00:09]
- key: `ORPHAN_SCAN|155 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-03T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=12 pred=0.2253 actual=0.0833 gap=+0.1420`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-03T06:00:09]
- key: `ROI_STAT|S01_NAKAANA1: n=137 hit%=31.4% hit_CI[Bonf]=[21.3,43.6]% ROI=0.83 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-03T06:00:09]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=40 hit%=22.5% ROI=0.57 (コスト 9,500/回収 5,400)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-03T06:00:09]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=26 hit%=30.8% ROI=1.03 (コスト 6,300/回収 6,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-03T06:00:09]
- key: `DRIFT_BUCKET|drift ≥+30%: n=30 hit%=23.3% ROI=0.51 (コスト 8,400/回収 4,310)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-03T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=22 pred=0.3216 actual=0.1818 gap=+0.1397`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-03T06:00:09]
- key: `ROI_STAT|S00: n=165 hit%=26.1% hit_CI[Bonf]=[17.5,36.9]% ROI=0.71 ROI_boot95=[0.51,0.92]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-03T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=165<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-03T06:00:09]
- key: `ROI_STAT|S02_TETSUBAN: n=74 hit%=28.4% hit_CI[Bonf]=[16.1,45.1]% ROI=0.44 ROI_boot95=[0.2`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-03T06:00:09]
- key: `DRIFT_BUCKET|drift ≤-30%: n=36 hit%=27.8% ROI=0.85 (コスト 10,500/回収 8,940)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-03T06:00:09]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=85 hit%=29.4% ROI=0.74 (コスト 19,900/回収 14,680)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-03T06:00:09]
- key: `CALIBRATION_LIVE|bt=win: n=376 pred=0.4808 actual=0.2846 error=+0.1962 (+41%) brier=0.2376 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.64MB / last modified 2026-07-03T13:49:37.261657+09:00

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
by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-03 13:49:06,617 [INFO] predictor: Models loaded OK
2026-07-03 13:49:19,155 [INFO] scraper: odds3t: 120/120 parsed
2026-07-03 13:49:20,236 [INFO] scraper: odds3f: 20/20 parsed
2026-07-03 13:49:21,346 [INFO] scraper: odds2t: 30/30 parsed
2026-07-03 13:49:21,347 [INFO] scraper: odds2f: 15/15 parsed
2026-07-03 13:49:22,419 [INFO] scraper: odds_win: 4/6 parsed
2026-07-03 13:49:22,420 [INFO] scraper: fetch_race 16/7: boats=6 odds=189/191
2026-07-03 13:49:22,432 [INFO] predictor: CALIBRATION_MODE=on
2026-07-03 13:49:22,432 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-07-03 13:49:22,439 [INFO] run_cycle: fetched 16/7 [final]: 154 combos
2026-07-03 13:49:25,898 [INFO] scraper: odds3t: 120/120 parsed
2026-07-03 13:49:27,000 [INFO] scraper: odds3f: 20/20 parsed
2026-07-03 13:49:28,098 [INFO] scraper: odds2t: 30/30 parsed
2026-07-03 13:49:28,099 [INFO] scraper: odds2f: 15/15 parsed
2026-07-03 13:49:29,195 [INFO] scraper: odds_win: 6/6 parsed
2026-07-03 13:49:29,196 [INFO] scraper: fetch_race 04/5: boats=6 odds=191/191
2026-07-03 13:49:29,205 [INFO] predictor: CALIBRATION_MODE=on
2026-07-03 13:49:29,205 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-03 13:49:29,213 [INFO] run_cycle: fetched 04/5 [scan]: 156 combos
2026-07-03 13:49:32,707 [INFO] scraper: odds3t: 120/120 parsed
2026-07-03 13:49:33,826 [INFO] scraper: odds3f: 20/20 parsed
2026-07-03 13:49:34,951 [INFO] scraper: odds2t: 30/30 parsed
2026-07-03 13:49:34,952 [INFO] scraper: odds2f: 15/15 parsed
2026-07-03 13:49:36,212 [INFO] scraper: odds_win: 6/6 parsed
2026-07-03 13:49:36,213 [INFO] scraper: fetch_race 13/8: boats=6 odds=191/191
2026-07-03 13:49:36,220 [INFO] predictor: CALIBRATION_MODE=on
2026-07-03 13:49:36,220 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-03 13:49:36,231 [INFO] run_cycle: fetched 13/8 [scan]: 156 combos
2026-07-03 13:49:36,455 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 61
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 61
  }
]
```

## Phase別通知記録 (24h)
{'final': 27, 'result': 10, 'scan': 24}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 38
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 10
  ANOMALY_SCRAPER_FAILURE_BURST: 7
  ANOMALY_BET_VOLUME_DROP: 6
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 38 | 10 | 11,400 | 7,710 | -3,690 | 0.676 |
| S01_NAKAANA1 | 37 | 12 | 7,400 | 5,820 | -1,580 | 0.786 |
| S02_TETSUBAN | 18 | 4 | 3,600 | 1,300 | -2,300 | 0.361 |

## 直近アラート (24h・新しい順)
```
[13:26:29] CIRCUIT_BREAKER_TRIP: {"cost": 11400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 38, "payout": 7710, "roi_7d": 0.676, "sid": "S00"}
[13:01:35] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:01:35] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[12:54:24] CIRCUIT_BREAKER_TRIP: {"cost": 11100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 7710, "roi_7d": 0.695, "sid": "S00"}
[12:51:23] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": -18.6, "final": 3.5, "kind": "LARGE_ODDS_DRIFT", "race": "043R", "scan": 4.3, "sid": "S01_NAKAANA1"}
[12:01:21] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:01:21] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[11:54:06] CIRCUIT_BREAKER_TRIP: {"cost": 11100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 7710, "roi_7d": 0.695, "sid": "S00"}
[11:50:35] CIRCUIT_BREAKER_TRIP: {"cost": 11400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 38, "payout": 7710, "roi_7d": 0.676, "sid": "S00"}
[11:35:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1030}
```

## 本日残レース: 99件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 69件 締切済
- 通知発射: scan=12 nid / final=15 nid / result=5 nid
- predictions: 7 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 065R | win | 1 | 0.4111 | 11.4 | 4.69 | 300 | scan=- drift=- | 13:26:21 |
| S02_TETSUBAN | 166R | win | 1 | 0.4111 | 2.2 | 0.90 | 200 | scan=- drift=- | 13:19:22 |
| S02_TETSUBAN | 116R | win | 1 | 0.5334 | 2.1 | 1.12 | 200 | scan=- drift=- | 12:57:33 |
| S01_NAKAANA1 | 043R | win | 1 | 0.2864 | 3.5 | 1.00 | 200 | scan=4.3 drift=-18.6% | 12:51:21 |
| S02_TETSUBAN | 094R | win | 1 | 0.5545 | 2.5 | 1.39 | 200 | scan=2.4 drift=+4.2% | 12:06:20 |
| S02_TETSUBAN | 162R | win | 1 | 0.4989 | 2.2 | 1.10 | 200 | scan=2.5 drift=-12.0% | 11:09:20 |
| S01_NAKAANA1 | 234R | win | 1 | 0.4989 | 3.7 | 1.85 | 200 | scan=3.4 drift=+8.8% | 09:59:45 |
| S00 | 194R | win | 1 | 0.4111 | 6.5 | 2.67 | 300 | scan=- drift=- | 17:04:46 |
| S02_TETSUBAN | 0510R | win | 1 | 0.5174 | 2.6 | 1.35 | 200 | scan=2.3 drift=+13.0% | 16:13:20 |
| S00 | 0610R | win | 1 | 0.4111 | 4.0 | 1.64 | 300 | scan=- drift=- | 16:05:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 58 | +8.9% | -68.9% | +584.6% | 22 | 11 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 459.7s |
| **Latency** (scan→final max) | 624.3s |
| **Traffic** (notifications 24h) | 61 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 375 | 0.4810 | 0.2853 | +0.1956 | 🟡+41% | 0.2381 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 164 | 0.4434 | 0.2622 | 0.2206 | 🔴-0.14 | 0.711 |
| S01_NAKAANA1 | win | 137 | 0.4930 | 0.3139 | 0.2418 | 🔴-0.12 | 0.831 |
| S02_TETSUBAN | win | 74 | 0.5421 | 0.2838 | 0.2698 | 🔴-0.33 | 0.459 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1780 | 0.2857 | 🔴-0.1077 |
| 0.20-0.30 | 13 | 0.2300 | 0.0769 | 🔴+0.1531 |
| 0.30-0.50 | 130 | 0.4228 | 0.2462 | 🔴+0.1767 |
| 0.50+ | 222 | 0.5445 | 0.3243 | 🔴+0.2201 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 50 | 0.733 |
| win | <5.0 | ✅learned | 111 | 0.716 |
| win | <10.0 | ✅learned | 62 | 0.486 |
| win | <20.0 | ✅learned | 18 | 0.212 |
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
_auto-generated by claude_snapshot.py at 2026-07-03T13:50:01.557064+09:00_