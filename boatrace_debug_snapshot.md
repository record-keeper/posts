# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-31T19:50:01.852164+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×27 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×47 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×27 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×3 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-31T19:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-31T19:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-31T19:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×43  [2026-08-31T19:07:20]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×129  [2026-08-31T19:07:20]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×43  [2026-08-31T19:07:20]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CALIBRATION_DRIFT  ×24  [2026-08-31T18:43:04]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×38  [2026-08-31T17:09:01]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×2  [2026-08-31T12:53:19]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-08-31T12:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×33  [2026-08-31T10:00:08]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-31T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=84<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-31T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S00: n=170<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-31T06:00:17]
- key: `ORPHAN_SCAN|198 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-31T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=12 pred=0.1819 actual=0.1667 gap=+0.0152`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-31T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=10 pred=0.1221 actual=0.1000 gap=+0.0221`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-31T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2251 actual=0.2222 gap=+0.0029`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-31T06:00:17]
- key: `ROI_STAT|S00: n=170 hit%=27.1% hit_CI[Bonf]=[18.5,37.8]% ROI=0.87 ROI_boot95=[0.63,1.15]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-31T06:00:17]
- key: `ROI_STAT|S01_NAKAANA1: n=183 hit%=24.6% hit_CI[Bonf]=[16.6,34.8]% ROI=0.75 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-31T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=183<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.96MB / last modified 2026-08-31T19:49:04.034127+09:00

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
lt=5000
2026-08-31 19:46:03,799 [INFO] predictor: Models loaded OK
2026-08-31 19:46:03,899 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-31 19:47:04,535 [INFO] run_cycle: === run_cycle 19:47:04 ===
2026-08-31 19:47:04,535 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-31 19:47:04,535 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-31 19:47:04,581 [INFO] predictor: Models loaded OK
2026-08-31 19:47:04,692 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-31 19:48:03,521 [INFO] run_cycle: === run_cycle 19:48:03 ===
2026-08-31 19:48:03,521 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-31 19:48:03,521 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-31 19:48:03,572 [INFO] predictor: Models loaded OK
2026-08-31 19:48:15,075 [INFO] scraper: odds3t: 120/120 parsed
2026-08-31 19:48:16,170 [INFO] scraper: odds3f: 20/20 parsed
2026-08-31 19:48:17,251 [INFO] scraper: odds2t: 30/30 parsed
2026-08-31 19:48:17,252 [INFO] scraper: odds2f: 15/15 parsed
2026-08-31 19:48:18,427 [INFO] scraper: odds_win: 4/6 parsed
2026-08-31 19:48:18,427 [INFO] scraper: fetch_race 07/11: boats=6 odds=189/191
2026-08-31 19:48:18,430 [INFO] predictor: CALIBRATION_MODE=on
2026-08-31 19:48:18,431 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-08-31 19:48:18,434 [INFO] run_cycle: fetched 07/11 [scan]: 154 combos
2026-08-31 19:48:18,540 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-31 19:49:03,596 [INFO] run_cycle: === run_cycle 19:49:03 ===
2026-08-31 19:49:03,596 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-31 19:49:03,596 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-31 19:49:03,625 [INFO] predictor: Models loaded OK
2026-08-31 19:49:03,718 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 64
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 64
  }
]
```

## Phase別通知記録 (24h)
{'final': 28, 'result': 13, 'scan': 23}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 169
  CIRCUIT_BREAKER_NO_ACTION: 51
  FINAL_MISSING: 47
  CIRCUIT_BREAKER_TRIP: 27
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 8
  CALIBRATION_DRIFT: 3
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 41 | 9 | 12,300 | 9,360 | -2,940 | 0.761 |
| S01_NAKAANA1 | 35 | 6 | 7,000 | 3,100 | -3,900 | 0.443 |
| S02_TETSUBAN | 20 | 8 | 4,000 | 3,420 | -580 | 0.855 |

## 直近アラート (24h・新しい順)
```
[19:44:20] FINAL_MISSING: {"deadline": "2026-08-31T12:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026083118081209", "sid": "S00"}
[19:34:37] FINAL_MISSING: {"deadline": "2026-08-31T18:04:00+09:00", "kind": "FINAL_MISSING", "nid": "2026083120071804", "sid": "S00"}
[19:22:18] FINAL_MISSING: {"deadline": "2026-08-31T11:48:00+09:00", "kind": "FINAL_MISSING", "nid": "2026083104011148", "sid": "S01_NAKAANA1"}
[19:22:18] FINAL_MISSING: {"deadline": "2026-08-31T11:48:00+09:00", "kind": "FINAL_MISSING", "nid": "2026083104011148", "sid": "S00"}
[19:07:20] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[19:07:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[19:07:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[19:07:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[19:01:25] CIRCUIT_BREAKER_TRIP: {"cost": 7000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 3100, "roi_7d": 0.443, "sid": "S01_NAKAANA1"}
[19:00:07] CALIBRATION_DRIFT: {"avg_actual": 0.2371, "avg_pred": 0.4777, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 97, "overconf_pct": 50.4}
```

## 本日残レース: 6件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 138件 締切済
- 通知発射: scan=21 nid / final=26 nid / result=12 nid
- predictions: 13 / うち結果DB記録済: 13
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 207R | win | 1 | 0.4111 | 4.0 | 1.64 | 200 | scan=4.9 drift=-18.4% | 18:01:20 |
| S00 | 204R | win | 1 | 0.5086 | 10.7 | 5.44 | 300 | scan=- drift=- | 16:36:18 |
| S01_NAKAANA1 | 204R | win | 1 | 0.5086 | 3.2 | 1.63 | 200 | scan=- drift=- | 16:35:19 |
| S00 | 0810R | win | 1 | 0.5891 | 4.0 | 2.36 | 300 | scan=- drift=- | 14:57:19 |
| S01_NAKAANA1 | 047R | win | 1 | 0.5123 | 4.0 | 2.05 | 200 | scan=- drift=- | 14:47:18 |
| S00 | 088R | win | 1 | 0.5735 | 4.5 | 2.58 | 300 | scan=- drift=- | 13:56:19 |
| S01_NAKAANA1 | 1811R | win | 1 | 0.5123 | 4.6 | 2.36 | 200 | scan=- drift=- | 13:47:20 |
| S01_NAKAANA1 | 045R | win | 1 | 0.3831 | 3.2 | 1.23 | 200 | scan=3.0 drift=+6.7% | 13:44:30 |
| S02_TETSUBAN | 2110R | win | 1 | 0.5990 | 2.1 | 1.26 | 200 | scan=- drift=- | 12:59:18 |
| S01_NAKAANA1 | 239R | win | 1 | 0.5735 | 4.3 | 2.47 | 200 | scan=3.9 drift=+10.3% | 12:33:29 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 55 | +6.2% | -73.3% | +158.3% | 17 | 7 | 40 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 464.8s |
| **Latency** (scan→final max) | 663.2s |
| **Traffic** (notifications 24h) | 64 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 1,400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 436 | 0.4729 | 0.2844 | +0.1885 | 🟡+40% | 0.2381 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 168 | 0.4166 | 0.2619 | 0.2116 | 🔴-0.09 | 0.846 |
| S01_NAKAANA1 | win | 185 | 0.4898 | 0.2432 | 0.2512 | 🔴-0.36 | 0.743 |
| S02_TETSUBAN | win | 83 | 0.5489 | 0.4217 | 0.2625 | 🔴-0.08 | 0.722 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 8 | 0.1250 | 0.0000 | 🔴+0.1250 |
| 0.15-0.20 | 12 | 0.1819 | 0.1667 | ✅+0.0152 |
| 0.20-0.30 | 9 | 0.2251 | 0.2222 | ✅+0.0029 |
| 0.30-0.50 | 148 | 0.4086 | 0.2432 | 🔴+0.1654 |
| 0.50+ | 257 | 0.5460 | 0.3268 | 🔴+0.2191 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 126 | 0.778 |
| win | <5.0 | ✅learned | 227 | 0.745 |
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
_auto-generated by claude_snapshot.py at 2026-08-31T19:50:01.852164+09:00_