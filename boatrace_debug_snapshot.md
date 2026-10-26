# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-27T02:50:01.429397+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×35 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×35 (24h)
- 🟡 FINAL_MISSING×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 SNAPSHOT_STALE×10 (24h)
- 🔴 SEND_WITHOUT_DBREC×8 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-27T02:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-27T02:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×14  [2026-10-26T23:46:03]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 SEND_WITHOUT_DBREC  ×14  [2026-10-26T23:46:03]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### 🔴 CIRCUIT_BREAKER_TRIP  ×50  [2026-10-26T23:10:05]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×100  [2026-10-26T23:10:05]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×50  [2026-10-26T23:10:05]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 SNAPSHOT_STALE  ×10  [2026-10-26T16:41:11]
- key: `SNAPSHOT_STALE|`
- **FIX**: snapshot が 20分以上古い→sync_snapshot_to_github.sh の cron と git push 権限確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×24  [2026-10-26T16:22:28]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_DROP  ×52  [2026-10-26T10:00:12]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-26T06:00:39]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=72<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-26T06:00:39]
- key: `ORPHAN_SCAN|163 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-26T06:00:39]
- key: `INSUFFICIENT_SAMPLE|S00: n=184<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-26T06:00:39]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=66 hit%=31.8% ROI=0.83 (コスト 15,700/回収 13,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-26T06:00:39]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1854 actual=0.0000 gap=+0.1854`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-26T06:00:39]
- key: `ROI_STAT|S00: n=184 hit%=29.9% hit_CI[Bonf]=[21.2,40.3]% ROI=0.80 ROI_boot95=[0.59,1.03]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-26T06:00:39]
- key: `ROI_STAT|S01_NAKAANA1: n=192 hit%=33.9% hit_CI[Bonf]=[24.9,44.2]% ROI=0.90 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-26T06:00:39]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=192<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-10-26T06:00:39]
- key: `ROI_STAT|S02_TETSUBAN: n=72 hit%=51.4% hit_CI[Bonf]=[35.1,67.3]% ROI=0.89 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-26T06:00:39]
- key: `DRIFT_BUCKET|drift ≤-30%: n=27 hit%=44.4% ROI=1.17 (コスト 7,800/回収 9,150)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.9MB / last modified 2026-10-27T02:30:03.877501+09:00

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
03 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-26 23:55:03,903 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-26 23:55:03,947 [INFO] predictor: Models loaded OK
2026-10-26 23:55:03,953 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-26 23:56:03,478 [INFO] run_cycle: === run_cycle 23:56:03 ===
2026-10-26 23:56:03,478 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-26 23:56:03,478 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-26 23:56:03,521 [INFO] predictor: Models loaded OK
2026-10-26 23:56:03,525 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-26 23:57:03,745 [INFO] run_cycle: === run_cycle 23:57:03 ===
2026-10-26 23:57:03,745 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-26 23:57:03,745 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-26 23:57:03,789 [INFO] predictor: Models loaded OK
2026-10-26 23:57:03,793 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-26 23:58:04,085 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-10-26 23:58:04,086 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-26 23:58:04,086 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-26 23:58:04,113 [INFO] predictor: Models loaded OK
2026-10-26 23:58:04,115 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-26 23:59:03,872 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-10-26 23:59:03,872 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-26 23:59:03,873 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-26 23:59:03,899 [INFO] predictor: Models loaded OK
2026-10-26 23:59:03,901 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 72
  }
]
```

## Phase別通知記録 (24h)
{'final': 31, 'result': 16, 'scan': 24}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 161
  CIRCUIT_BREAKER_TRIP: 35
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_SCAN_FINAL_RATIO: 33
  FINAL_MISSING: 20
  STRATEGY_CI_FAIL: 17
  SNAPSHOT_STALE: 10
  SEND_WITHOUT_DBREC: 8
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 44 | 13 | 13,200 | 10,230 | -2,970 | 0.775 |
| S01_NAKAANA1 | 49 | 10 | 9,800 | 3,760 | -6,040 | 0.384 |
| S02_TETSUBAN | 11 | 6 | 2,200 | 1,980 | -220 | 0.9 |

## 直近アラート (24h・新しい順)
```
[23:50:04] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.213, "baseline_mean": 0.787, "baseline_stdev": 0.053, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 20, "z_score": 3.98}
[23:45:03] FINAL_MISSING: {"deadline": "2026-10-26T15:05:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102622091505", "sid": "S00"}
[23:45:03] FINAL_MISSING: {"deadline": "2026-10-26T13:05:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102606061305", "sid": "S00"}
[23:45:03] SEND_WITHOUT_DBREC: {"kind": "SEND_WITHOUT_DBREC", "nid": "2026102615031606", "phase": "result", "sid": "S01_NAKAANA1"}
[23:29:04] CIRCUIT_BREAKER_TRIP: {"cost": 9800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 49, "payout": 3760, "roi_7d": 0.384, "sid": "S01_NAKAANA1"}
[23:10:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:10:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:10:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[22:49:04] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.213, "baseline_mean": 0.787, "baseline_stdev": 0.053, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 20, "z_score": 3.98}
[22:44:04] FINAL_MISSING: {"deadline": "2026-10-26T15:05:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102622091505", "sid": "S00"}
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
| S01_NAKAANA1 | 1511R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=- drift=- | 19:56:19 |
| S01_NAKAANA1 | 014R | win | 1 | 0.5334 | 3.6 | 1.92 | 200 | scan=4.6 drift=-21.7% | 16:45:21 |
| S01_NAKAANA1 | 153R | win | 1 | 0.5123 | 3.7 | 1.90 | 200 | scan=4.5 drift=-17.8% | 16:03:23 |
| S02_TETSUBAN | 1112R | win | 1 | 0.5735 | 2.3 | 1.32 | 200 | scan=2.3 drift=+0.0% | 15:56:18 |
| S01_NAKAANA1 | 011R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=- drift=- | 15:19:20 |
| S02_TETSUBAN | 1110R | win | 1 | 0.5891 | 2.0 | 1.18 | 200 | scan=- drift=- | 14:43:19 |
| S00 | 049R | win | 1 | 0.4989 | 7.8 | 3.89 | 300 | scan=6.7 drift=+16.4% | 14:38:19 |
| S02_TETSUBAN | 059R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=- drift=- | 14:28:31 |
| S00 | 046R | win | 1 | 0.4111 | 10.2 | 4.19 | 300 | scan=24.7 drift=-58.7% | 13:10:23 |
| S00 | 225R | win | 1 | 0.4111 | 16.0 | 6.58 | 300 | scan=- drift=- | 12:56:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 50 | +13.6% | -77.4% | +369.8% | 13 | 4 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 441.1s |
| **Latency** (scan→final max) | 654.4s |
| **Traffic** (notifications 24h) | 71 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 455 | 0.4794 | 0.3516 | +0.1277 | 🟡+27% | 0.2393 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 189 | 0.4434 | 0.3016 | 0.2348 | 🔴-0.11 | 0.822 |
| S01_NAKAANA1 | win | 193 | 0.4891 | 0.3368 | 0.2378 | 🔴-0.06 | 0.894 |
| S02_TETSUBAN | win | 73 | 0.5466 | 0.5205 | 0.2551 | 🔴-0.02 | 0.904 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1865 | 0.0000 | 🔴+0.1865 |
| 0.20-0.30 | 9 | 0.2288 | 0.2222 | ✅+0.0066 |
| 0.30-0.50 | 159 | 0.4123 | 0.3145 | 🔴+0.0978 |
| 0.50+ | 273 | 0.5432 | 0.3883 | 🔴+0.1549 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 195 | 0.778 |
| win | <5.0 | ✅learned | 352 | 0.74 |
| win | <10.0 | ✅learned | 155 | 0.451 |
| win | <20.0 | ✅learned | 45 | 0.254 |
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
_auto-generated by claude_snapshot.py at 2026-10-27T02:50:01.429397+09:00_