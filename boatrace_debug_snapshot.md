# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-30T22:10:01.352525+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×37 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×39 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×37 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×2 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×1  [2026-08-30T22:09:05]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-30T22:09:05]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×1  [2026-08-30T22:09:05]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-30T22:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-30T22:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-30T22:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×6  [2026-08-30T19:47:28]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×35  [2026-08-30T16:53:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CALIBRATION_DRIFT  ×17  [2026-08-30T15:11:33]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-08-30T15:02:16]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### 🟡 ANOMALY_BET_VOLUME_DROP  ×27  [2026-08-30T14:03:19]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ORPHAN_SCAN  ×1  [2026-08-30T06:00:10]
- key: `ORPHAN_SCAN|195 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-30T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=83<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-30T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=171<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-30T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=30.2% ROI=0.94 (コスト 10,000/回収 9,380)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-30T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=12 pred=0.1819 actual=0.1667 gap=+0.0152`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-30T06:00:10]
- key: `ROI_STAT|S00: n=171 hit%=26.9% hit_CI[Bonf]=[18.4,37.6]% ROI=0.87 ROI_boot95=[0.62,1.15]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-30T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=188 hit%=25.5% hit_CI[Bonf]=[17.5,35.6]% ROI=0.81 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-30T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=188<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-30T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=83 hit%=39.8% hit_CI[Bonf]=[25.9,55.5]% ROI=0.66 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.86MB / last modified 2026-08-30T22:09:05.478155+09:00

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
43 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-30 22:05:04,244 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-30 22:05:04,292 [INFO] predictor: Models loaded OK
2026-08-30 22:05:04,297 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-30 22:06:04,081 [INFO] run_cycle: === run_cycle 22:06:04 ===
2026-08-30 22:06:04,081 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-30 22:06:04,081 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-30 22:06:04,152 [INFO] predictor: Models loaded OK
2026-08-30 22:06:04,158 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-30 22:07:04,461 [INFO] run_cycle: === run_cycle 22:07:04 ===
2026-08-30 22:07:04,461 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-30 22:07:04,461 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-30 22:07:04,507 [INFO] predictor: Models loaded OK
2026-08-30 22:07:04,512 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-30 22:08:03,894 [INFO] run_cycle: === run_cycle 22:08:03 ===
2026-08-30 22:08:03,894 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-30 22:08:03,894 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-30 22:08:03,970 [INFO] predictor: Models loaded OK
2026-08-30 22:08:03,974 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-30 22:09:04,775 [INFO] run_cycle: === run_cycle 22:09:04 ===
2026-08-30 22:09:04,775 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-30 22:09:04,775 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-30 22:09:04,856 [INFO] predictor: Models loaded OK
2026-08-30 22:09:04,860 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 45
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 45
  }
]
```

## Phase別通知記録 (24h)
{'final': 18, 'result': 9, 'scan': 18}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 92
  CIRCUIT_BREAKER_NO_ACTION: 42
  FINAL_MISSING: 39
  CIRCUIT_BREAKER_TRIP: 37
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 14
  ANOMALY_BET_VOLUME_DROP: 7
  CALIBRATION_DRIFT: 2
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 40 | 8 | 12,000 | 8,520 | -3,480 | 0.71 |
| S01_NAKAANA1 | 33 | 8 | 6,600 | 3,680 | -2,920 | 0.558 |
| S02_TETSUBAN | 21 | 8 | 4,200 | 3,420 | -780 | 0.814 |

## 直近アラート (24h・新しい順)
```
[22:09:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[22:09:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[22:09:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[22:04:04] FINAL_MISSING: {"deadline": "2026-08-30T18:31:00+09:00", "kind": "FINAL_MISSING", "nid": "2026083007081831", "sid": "S00"}
[22:00:06] FINAL_MISSING: {"deadline": "2026-08-30T12:25:00+09:00", "kind": "FINAL_MISSING", "nid": "2026083021091225", "sid": "S00"}
[21:54:03] FINAL_MISSING: {"deadline": "2026-08-30T12:17:00+09:00", "kind": "FINAL_MISSING", "nid": "2026083004021217", "sid": "S00"}
[21:35:04] FINAL_MISSING: {"deadline": "2026-08-30T13:00:00+09:00", "kind": "FINAL_MISSING", "nid": "2026083005041300", "sid": "S00"}
[21:24:04] FINAL_MISSING: {"deadline": "2026-08-30T15:52:00+09:00", "kind": "FINAL_MISSING", "nid": "2026083004091552", "sid": "S00"}
[21:23:04] CIRCUIT_BREAKER_TRIP: {"cost": 6600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 33, "payout": 3680, "roi_7d": 0.558, "sid": "S01_NAKAANA1"}
[21:23:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 168件 締切済
- 通知発射: scan=18 nid / final=17 nid / result=8 nid
- predictions: 9 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 079R | win | 1 | 0.5123 | 2.5 | 1.28 | 200 | scan=- drift=- | 19:00:21 |
| S00 | 196R | win | 1 | 0.5123 | 5.5 | 2.82 | 300 | scan=- drift=- | 17:40:19 |
| S00 | 048R | win | 1 | 0.4111 | 12.4 | 5.10 | 300 | scan=4.8 drift=+158.3% | 15:19:25 |
| S00 | 0810R | win | 1 | 0.5891 | 4.5 | 2.65 | 300 | scan=14.0 drift=-67.9% | 15:07:19 |
| S01_NAKAANA1 | 099R | win | 1 | 0.3177 | 4.0 | 1.27 | 200 | scan=3.0 drift=+33.3% | 14:30:30 |
| S00 | 099R | win | 1 | 0.3177 | 4.0 | 1.27 | 300 | scan=- drift=- | 14:30:28 |
| S00 | 166R | win | 1 | 0.3177 | 11.2 | 3.56 | 300 | scan=5.2 drift=+115.4% | 13:49:18 |
| S02_TETSUBAN | 117R | win | 1 | 0.5123 | 2.3 | 1.18 | 200 | scan=- drift=- | 13:41:30 |
| S01_NAKAANA1 | 164R | win | 1 | 0.5476 | 3.0 | 1.64 | 200 | scan=- drift=- | 12:47:30 |
| S00 | 192R | win | 1 | 0.1084 | 5.5 | 0.60 | 300 | scan=5.6 drift=-1.8% | 15:46:30 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 56 | +4.0% | -73.3% | +158.3% | 19 | 9 | 41 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 533.9s |
| **Latency** (scan→final max) | 660.8s |
| **Traffic** (notifications 24h) | 45 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 437 | 0.4718 | 0.2883 | +0.1835 | 🟡+39% | 0.2394 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 170 | 0.4137 | 0.2706 | 0.2162 | 🔴-0.10 | 0.872 |
| S01_NAKAANA1 | win | 183 | 0.4908 | 0.2459 | 0.2506 | 🔴-0.35 | 0.751 |
| S02_TETSUBAN | win | 84 | 0.5480 | 0.4167 | 0.2620 | 🔴-0.08 | 0.713 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1221 | 0.1000 | ✅+0.0221 |
| 0.15-0.20 | 12 | 0.1819 | 0.1667 | ✅+0.0152 |
| 0.20-0.30 | 9 | 0.2251 | 0.2222 | ✅+0.0029 |
| 0.30-0.50 | 147 | 0.4100 | 0.2449 | 🔴+0.1651 |
| 0.50+ | 257 | 0.5460 | 0.3307 | 🔴+0.2152 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 126 | 0.778 |
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
_auto-generated by claude_snapshot.py at 2026-08-30T22:10:01.352525+09:00_