# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-05T12:10:01.458186+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×37 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×69 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×37 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×8 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×7  [2026-08-05T12:03:27]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×14  [2026-08-05T12:03:27]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×7  [2026-08-05T12:03:27]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×5  [2026-08-05T11:50:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-05T11:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-05T11:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-05T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=69<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-05T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=178<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-05T06:00:07]
- key: `ORPHAN_SCAN|173 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-05T06:00:07]
- key: `DRIFT_BUCKET|drift ≥+30%: n=40 hit%=25.0% ROI=0.88 (コスト 11,100/回収 9,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-05T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2244 actual=0.4000 gap=-0.1756`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-05T06:00:07]
- key: `ROI_STAT|S00: n=178 hit%=25.8% hit_CI[Bonf]=[17.6,36.2]% ROI=0.69 ROI_boot95=[0.48,0.93]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-05T06:00:07]
- key: `ROI_STAT|S01_NAKAANA1: n=157 hit%=23.6% hit_CI[Bonf]=[15.3,34.5]% ROI=0.70 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-05T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=157<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-05T06:00:07]
- key: `ROI_STAT|S02_TETSUBAN: n=69 hit%=49.3% hit_CI[Bonf]=[32.9,65.8]% ROI=0.96 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-05T06:00:07]
- key: `DRIFT_BUCKET|drift ≤-30%: n=36 hit%=22.2% ROI=0.53 (コスト 10,600/回収 5,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-05T06:00:07]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=34 hit%=38.2% ROI=0.92 (コスト 8,500/回収 7,820)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-05T06:00:07]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=66 hit%=31.8% ROI=0.76 (コスト 15,500/回収 11,710)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-05T06:00:07]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=42 hit%=21.4% ROI=0.42 (コスト 9,800/回収 4,080)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-05T06:00:07]
- key: `CALIBRATION_LIVE|bt=win: n=404 pred=0.4593 actual=0.2896 error=+0.1697 (+37%) brier=0.2327 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 9.5MB / last modified 2026-08-05T12:09:04.579682+09:00

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
08-05 12:06:36,697 [INFO] run_cycle: fetched 06/3 [scan]: 154 combos
2026-08-05 12:06:36,811 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-05 12:07:03,423 [INFO] run_cycle: === run_cycle 12:07:03 ===
2026-08-05 12:07:03,423 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-05 12:07:03,423 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-05 12:07:03,470 [INFO] predictor: Models loaded OK
2026-08-05 12:07:03,657 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-05 12:08:03,884 [INFO] run_cycle: === run_cycle 12:08:03 ===
2026-08-05 12:08:03,884 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-05 12:08:03,884 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-05 12:08:03,930 [INFO] predictor: Models loaded OK
2026-08-05 12:08:15,592 [INFO] scraper: odds3t: 120/120 parsed
2026-08-05 12:08:16,711 [INFO] scraper: odds3f: 20/20 parsed
2026-08-05 12:08:17,797 [INFO] scraper: odds2t: 30/30 parsed
2026-08-05 12:08:17,799 [INFO] scraper: odds2f: 14/15 parsed
2026-08-05 12:08:18,902 [INFO] scraper: odds_win: 4/6 parsed
2026-08-05 12:08:18,902 [INFO] scraper: fetch_race 10/9: boats=6 odds=188/191
2026-08-05 12:08:18,905 [INFO] predictor: CALIBRATION_MODE=on
2026-08-05 12:08:18,906 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-08-05 12:08:18,909 [INFO] run_cycle: fetched 10/9 [scan]: 154 combos
2026-08-05 12:08:19,011 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-05 12:09:03,659 [INFO] run_cycle: === run_cycle 12:09:03 ===
2026-08-05 12:09:03,660 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-05 12:09:03,660 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-05 12:09:03,708 [INFO] predictor: Models loaded OK
2026-08-05 12:09:03,922 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 58
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 58
  }
]
```

## Phase別通知記録 (24h)
{'final': 23, 'result': 10, 'scan': 25}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 125
  FINAL_MISSING: 69
  CIRCUIT_BREAKER_TRIP: 37
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 8
  PSI_DRIFT_DETECTED: 8
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 39 | 11 | 11,700 | 8,700 | -3,000 | 0.744 |
| S01_NAKAANA1 | 35 | 7 | 7,000 | 4,360 | -2,640 | 0.623 |
| S02_TETSUBAN | 14 | 7 | 2,800 | 2,140 | -660 | 0.764 |

## 直近アラート (24h・新しい順)
```
[12:03:26] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:03:26] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[12:03:26] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[11:56:26] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": -13.3, "final": 5.2, "kind": "LARGE_ODDS_DRIFT", "race": "094R", "scan": 6.0, "sid": "S00"}
[11:54:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 948}
[11:53:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 931}
[11:52:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 922}
[11:51:43] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 923}
[11:50:41] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 921}
[11:41:26] CIRCUIT_BREAKER_TRIP: {"cost": 7000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 4360, "roi_7d": 0.623, "sid": "S01_NAKAANA1"}
```

## 本日残レース: 97件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 35件 締切済
- 通知発射: scan=6 nid / final=7 nid / result=2 nid
- predictions: 4 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 094R | win | 1 | 0.3177 | 5.2 | 1.65 | 300 | scan=6.0 drift=-13.3% | 11:56:18 |
| S01_NAKAANA1 | 172R | win | 1 | 0.5719 | 3.3 | 1.89 | 200 | scan=- drift=- | 11:41:18 |
| S00 | 216R | win | 1 | 0.5476 | 4.7 | 2.57 | 300 | scan=4.7 drift=+0.0% | 10:51:42 |
| S02_TETSUBAN | 211R | win | 1 | 0.5476 | 2.0 | 1.10 | 200 | scan=- drift=- | 08:37:18 |
| S01_NAKAANA1 | 198R | win | 1 | 0.4111 | 4.1 | 1.69 | 200 | scan=3.2 drift=+28.1% | 18:40:45 |
| S00 | 198R | win | 1 | 0.4111 | 4.1 | 1.69 | 300 | scan=- drift=- | 18:40:44 |
| S00 | 196R | win | 1 | 0.5123 | 6.3 | 3.23 | 300 | scan=23.6 drift=-73.3% | 17:43:30 |
| S01_NAKAANA1 | 047R | win | 1 | 0.3177 | 3.6 | 1.14 | 200 | scan=3.1 drift=+16.1% | 14:55:19 |
| S01_NAKAANA1 | 056R | win | 1 | 0.3177 | 3.4 | 1.08 | 200 | scan=- drift=- | 14:00:24 |
| S01_NAKAANA1 | 045R | win | 1 | 0.4111 | 3.3 | 1.36 | 200 | scan=- drift=- | 13:52:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 55 | +10.1% | -73.3% | +375.6% | 18 | 12 | 39 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 505.1s |
| **Latency** (scan→final max) | 646.4s |
| **Traffic** (notifications 24h) | 58 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 404 | 0.4599 | 0.2946 | +0.1654 | 🟡+36% | 0.2329 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 179 | 0.4158 | 0.2626 | 0.2221 | 🔴-0.15 | 0.71 |
| S01_NAKAANA1 | win | 156 | 0.4797 | 0.2372 | 0.2396 | 🔴-0.32 | 0.706 |
| S02_TETSUBAN | win | 69 | 0.5296 | 0.5072 | 0.2456 | ✅+0.02 | 0.977 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 12 | 0.1235 | 0.1667 | ✅-0.0432 |
| 0.15-0.20 | 10 | 0.1823 | 0.2000 | ✅-0.0177 |
| 0.20-0.30 | 10 | 0.2244 | 0.4000 | 🔴-0.1756 |
| 0.30-0.50 | 156 | 0.4187 | 0.2179 | 🔴+0.2007 |
| 0.50+ | 212 | 0.5405 | 0.3632 | 🔴+0.1773 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 96 | 0.787 |
| win | <5.0 | ✅learned | 168 | 0.722 |
| win | <10.0 | ✅learned | 88 | 0.449 |
| win | <20.0 | ✅learned | 28 | 0.219 |
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
_auto-generated by claude_snapshot.py at 2026-08-05T12:10:01.458186+09:00_