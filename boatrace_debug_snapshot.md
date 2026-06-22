# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-23T02:20:01.627619+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×30 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×44 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×30 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-23T01:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-23T01:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×100  [2026-06-22T23:10:14]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×100  [2026-06-22T23:10:14]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×50  [2026-06-22T23:10:14]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×20  [2026-06-22T15:43:09]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-06-22T15:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×20  [2026-06-22T12:58:39]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×41  [2026-06-22T10:00:26]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-22T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=141<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-22T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=149<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-22T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-22T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2241 actual=0.1111 gap=+0.1130`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-22T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0816 actual=0.0000 gap=+0.0816`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-22T06:00:12]
- key: `ROI_STAT|S00: n=149 hit%=26.2% hit_CI[Bonf]=[17.2,37.6]% ROI=0.71 ROI_boot95=[0.51,0.95]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-22T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=141 hit%=27.7% hit_CI[Bonf]=[18.3,39.5]% ROI=0.73 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-22T06:00:12]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=35.0% hit_CI[Bonf]=[21.7,51.1]% ROI=0.59 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-22T06:00:12]
- key: `ORPHAN_SCAN|156 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-22T06:00:12]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=20.6% ROI=0.67 (コスト 9,700/回収 6,510)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-22T06:00:12]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=20.0% ROI=0.44 (コスト 8,000/回収 3,510)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.71MB / last modified 2026-06-23T02:00:10.764117+09:00

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
2026-06-22 23:55:07,362 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-22 23:55:07,412 [INFO] predictor: Models loaded OK
2026-06-22 23:55:07,416 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-22 23:56:04,673 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-06-22 23:56:04,673 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-22 23:56:04,673 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-22 23:56:04,747 [INFO] predictor: Models loaded OK
2026-06-22 23:56:04,753 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-22 23:57:06,316 [INFO] run_cycle: === run_cycle 23:57:06 ===
2026-06-22 23:57:06,317 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-22 23:57:06,317 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-22 23:57:06,361 [INFO] predictor: Models loaded OK
2026-06-22 23:57:06,365 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-22 23:58:06,289 [INFO] run_cycle: === run_cycle 23:58:06 ===
2026-06-22 23:58:06,289 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-22 23:58:06,289 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-22 23:58:06,334 [INFO] predictor: Models loaded OK
2026-06-22 23:58:06,341 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-22 23:59:06,505 [INFO] run_cycle: === run_cycle 23:59:06 ===
2026-06-22 23:59:06,505 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-22 23:59:06,505 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-22 23:59:06,548 [INFO] predictor: Models loaded OK
2026-06-22 23:59:06,553 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 18, 'result': 9, 'scan': 20}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 146
  FINAL_MISSING: 44
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 30
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 2
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 40 | 10 | 12,000 | 8,010 | -3,990 | 0.667 |
| S01_NAKAANA1 | 35 | 7 | 7,000 | 3,100 | -3,900 | 0.443 |
| S02_TETSUBAN | 14 | 5 | 2,800 | 1,920 | -880 | 0.686 |

## 直近アラート (24h・新しい順)
```
[23:40:08] CIRCUIT_BREAKER_TRIP: {"cost": 12000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 8010, "roi_7d": 0.667, "sid": "S00"}
[23:19:06] FINAL_MISSING: {"deadline": "2026-06-22T13:43:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062216061343", "sid": "S00"}
[23:19:06] FINAL_MISSING: {"deadline": "2026-06-22T15:45:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062215021545", "sid": "S01_NAKAANA1"}
[23:19:06] FINAL_MISSING: {"deadline": "2026-06-22T15:45:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062215021545", "sid": "S00"}
[23:19:06] FINAL_MISSING: {"deadline": "2026-06-22T14:44:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062211091444", "sid": "S02_TETSUBAN"}
[23:10:09] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:10:09] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:10:09] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:02:05] FINAL_MISSING: {"deadline": "2026-06-22T14:27:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062222051427", "sid": "S00"}
[23:00:12] CIRCUIT_BREAKER_TRIP: {"cost": 7000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 3100, "roi_7d": 0.443, "sid": "S01_NAKAANA1"}
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
| S00 | 156R | win | 1 | 0.4111 | 7.2 | 2.96 | 300 | scan=9.7 drift=-25.8% | 17:35:23 |
| S00 | 193R | win | 1 | 0.5891 | 12.3 | 7.25 | 300 | scan=4.1 drift=+200.0% | 16:20:35 |
| S00 | 167R | win | 1 | 0.5174 | 12.5 | 6.47 | 300 | scan=6.0 drift=+108.3% | 14:11:25 |
| S01_NAKAANA1 | 055R | win | 1 | 0.3177 | 4.3 | 1.37 | 200 | scan=- drift=- | 13:30:32 |
| S00 | 055R | win | 1 | 0.3177 | 4.3 | 1.37 | 300 | scan=- drift=- | 13:30:29 |
| S00 | 1011R | win | 1 | 0.5174 | 7.6 | 3.93 | 300 | scan=6.3 drift=+20.6% | 13:21:22 |
| S00 | 222R | win | 1 | 0.3177 | 26.2 | 8.32 | 300 | scan=4.5 drift=+482.2% | 12:58:23 |
| S01_NAKAANA1 | 084R | win | 1 | 0.4111 | 4.1 | 1.69 | 200 | scan=- drift=- | 11:54:20 |
| S01_NAKAANA1 | 106R | win | 1 | 0.5714 | 3.7 | 2.11 | 200 | scan=3.5 drift=+5.7% | 10:41:22 |
| S01_NAKAANA1 | 203R | win | 1 | 0.4989 | 3.8 | 1.90 | 200 | scan=3.0 drift=+26.7% | 18:31:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 52 | +10.0% | -61.4% | +482.2% | 19 | 8 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 511.8s |
| **Latency** (scan→final max) | 605.7s |
| **Traffic** (notifications 24h) | 47 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 368 | 0.4734 | 0.2772 | +0.1962 | 🟡+41% | 0.2407 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 153 | 0.4265 | 0.2484 | 0.2241 | 🔴-0.20 | 0.67 |
| S01_NAKAANA1 | win | 139 | 0.4887 | 0.2734 | 0.2436 | 🔴-0.23 | 0.727 |
| S02_TETSUBAN | win | 76 | 0.5397 | 0.3421 | 0.2689 | 🔴-0.19 | 0.582 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0816 | 0.0000 | 🔴+0.0816 |
| 0.15-0.20 | 7 | 0.1808 | 0.4286 | 🔴-0.2478 |
| 0.20-0.30 | 9 | 0.2241 | 0.1111 | 🔴+0.1130 |
| 0.30-0.50 | 125 | 0.4229 | 0.2240 | 🔴+0.1989 |
| 0.50+ | 216 | 0.5425 | 0.3194 | 🔴+0.2230 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 46 | 0.733 |
| win | <5.0 | ✅learned | 88 | 0.737 |
| win | <10.0 | ✅learned | 56 | 0.499 |
| win | <20.0 | ✅learned | 15 | 0.207 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-06-23T02:20:01.627619+09:00_