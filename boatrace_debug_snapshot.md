# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-30T05:50:01.725787+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×37 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×37 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-30T05:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-30T05:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×40  [2026-08-29T23:20:06]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×104  [2026-08-29T23:08:04]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×104  [2026-08-29T23:08:04]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×52  [2026-08-29T23:08:04]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×21  [2026-08-29T20:37:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-08-29T18:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-08-29T12:55:26]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### 🟡 ANOMALY_BET_VOLUME_DROP  ×23  [2026-08-29T10:00:51]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-29T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=79<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-29T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=171<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-29T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2255 actual=0.3000 gap=-0.0745`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-29T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=187<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-29T06:00:11]
- key: `ORPHAN_SCAN|198 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ ROI_STAT  ×1  [2026-08-29T06:00:11]
- key: `ROI_STAT|S00: n=171 hit%=26.9% hit_CI[Bonf]=[18.4,37.6]% ROI=0.90 ROI_boot95=[0.63,1.18]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-29T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=187 hit%=25.1% hit_CI[Bonf]=[17.2,35.2]% ROI=0.80 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-29T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=79 hit%=40.5% hit_CI[Bonf]=[26.2,56.6]% ROI=0.66 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-29T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=39 hit%=17.9% ROI=0.61 (コスト 11,300/回収 6,860)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-29T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=30.2% ROI=0.94 (コスト 10,000/回収 9,380)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.79MB / last modified 2026-08-30T05:30:03.852009+09:00

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
62 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-29 23:55:04,762 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-29 23:55:04,792 [INFO] predictor: Models loaded OK
2026-08-29 23:55:04,794 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-29 23:56:04,494 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-08-29 23:56:04,494 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-29 23:56:04,494 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-29 23:56:04,555 [INFO] predictor: Models loaded OK
2026-08-29 23:56:04,560 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-29 23:57:04,061 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-08-29 23:57:04,061 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-29 23:57:04,061 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-29 23:57:04,109 [INFO] predictor: Models loaded OK
2026-08-29 23:57:04,115 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-29 23:58:03,407 [INFO] run_cycle: === run_cycle 23:58:03 ===
2026-08-29 23:58:03,408 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-29 23:58:03,408 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-29 23:58:03,458 [INFO] predictor: Models loaded OK
2026-08-29 23:58:03,463 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-29 23:59:03,606 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-08-29 23:59:03,606 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-29 23:59:03,606 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-29 23:59:03,638 [INFO] predictor: Models loaded OK
2026-08-29 23:59:03,640 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 47
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 47
  }
]
```

## Phase別通知記録 (24h)
{'final': 20, 'result': 12, 'scan': 15}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 105
  CIRCUIT_BREAKER_TRIP: 37
  CIRCUIT_BREAKER_NO_ACTION: 29
  ANOMALY_SCAN_FINAL_RATIO: 24
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 9 | 12,600 | 9,780 | -2,820 | 0.776 |
| S01_NAKAANA1 | 44 | 10 | 8,800 | 4,940 | -3,860 | 0.561 |
| S02_TETSUBAN | 20 | 6 | 4,000 | 2,460 | -1,540 | 0.615 |

## 直近アラート (24h・新しい順)
```
[23:44:04] CIRCUIT_BREAKER_TRIP: {"cost": 4000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 20, "payout": 2460, "roi_7d": 0.615, "sid": "S02_TETSUBAN"}
[23:35:04] CIRCUIT_BREAKER_TRIP: {"cost": 8800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 44, "payout": 4940, "roi_7d": 0.561, "sid": "S01_NAKAANA1"}
[23:31:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[23:08:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:08:03] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:02:04] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.2, "baseline_mean": 0.8, "baseline_stdev": 0.047, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 15, "z_score": 4.22}
[22:43:03] CIRCUIT_BREAKER_TRIP: {"cost": 4000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 20, "payout": 2460, "roi_7d": 0.615, "sid": "S02_TETSUBAN"}
[22:35:04] CIRCUIT_BREAKER_TRIP: {"cost": 8800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 44, "payout": 4940, "roi_7d": 0.561, "sid": "S01_NAKAANA1"}
[22:30:09] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[22:07:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 0件 登録 / 0件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 192R | win | 1 | 0.1084 | 5.5 | 0.60 | 300 | scan=5.6 drift=-1.8% | 15:46:30 |
| S02_TETSUBAN | 059R | win | 1 | 0.4989 | 2.6 | 1.30 | 200 | scan=- drift=- | 15:35:30 |
| S01_NAKAANA1 | 057R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=- drift=- | 14:29:25 |
| S01_NAKAANA1 | 045R | win | 1 | 0.5174 | 3.0 | 1.55 | 200 | scan=3.0 drift=+0.0% | 13:44:44 |
| S01_NAKAANA1 | 137R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=3.6 drift=+22.2% | 13:36:18 |
| S02_TETSUBAN | 117R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=2.0 drift=+5.0% | 13:23:31 |
| S01_NAKAANA1 | 115R | win | 1 | 0.4989 | 3.3 | 1.65 | 200 | scan=- drift=- | 12:27:19 |
| S02_TETSUBAN | 053R | win | 1 | 0.5174 | 2.6 | 1.35 | 200 | scan=2.1 drift=+23.8% | 12:24:20 |
| S02_TETSUBAN | 163R | win | 1 | 0.5891 | 2.0 | 1.18 | 200 | scan=- drift=- | 12:15:26 |
| S02_TETSUBAN | 112R | win | 1 | 0.5891 | 2.4 | 1.41 | 200 | scan=- drift=- | 10:59:43 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 63 | +3.5% | -79.6% | +320.7% | 22 | 10 | 45 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 514.6s |
| **Latency** (scan→final max) | 611.6s |
| **Traffic** (notifications 24h) | 47 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 442 | 0.4728 | 0.2873 | +0.1854 | 🟡+39% | 0.2400 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 171 | 0.4153 | 0.2690 | 0.2172 | 🔴-0.10 | 0.867 |
| S01_NAKAANA1 | win | 188 | 0.4920 | 0.2553 | 0.2511 | 🔴-0.32 | 0.813 |
| S02_TETSUBAN | win | 83 | 0.5475 | 0.3976 | 0.2617 | 🔴-0.09 | 0.664 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1221 | 0.1000 | ✅+0.0221 |
| 0.15-0.20 | 12 | 0.1819 | 0.1667 | ✅+0.0152 |
| 0.20-0.30 | 9 | 0.2251 | 0.2222 | ✅+0.0029 |
| 0.30-0.50 | 151 | 0.4138 | 0.2450 | 🔴+0.1688 |
| 0.50+ | 258 | 0.5460 | 0.3295 | 🔴+0.2166 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 124 | 0.775 |
| win | <5.0 | ✅learned | 225 | 0.745 |
| win | <10.0 | ✅learned | 109 | 0.458 |
| win | <20.0 | ✅learned | 30 | 0.227 |
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
_auto-generated by claude_snapshot.py at 2026-08-30T05:50:01.725787+09:00_