# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-22T13:20:01.437494+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×30 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×42 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×30 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×17  [2026-06-22T13:03:57]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×34  [2026-06-22T13:03:57]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×17  [2026-06-22T13:03:57]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×13  [2026-06-22T12:58:39]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-22T12:30:09]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-22T12:30:09]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×56  [2026-06-22T12:24:42]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

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

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-22T06:00:12]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=76 hit%=30.3% ROI=0.71 (コスト 18,100/回収 12,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.68MB / last modified 2026-06-22T13:19:36.502199+09:00

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
ls loaded OK
2026-06-22 13:18:17,159 [WARNING] scraper: beforeinfo parse failed: jcd=08 rno=7
2026-06-22 13:18:17,160 [WARNING] run_cycle: fetch None: 08/7
2026-06-22 13:18:17,251 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-22 13:19:05,727 [INFO] run_cycle: === run_cycle 13:19:05 ===
2026-06-22 13:19:05,727 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-22 13:19:05,727 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-22 13:19:05,788 [INFO] predictor: Models loaded OK
2026-06-22 13:19:18,317 [INFO] scraper: odds3t: 120/120 parsed
2026-06-22 13:19:19,541 [INFO] scraper: odds3f: 20/20 parsed
2026-06-22 13:19:20,876 [INFO] scraper: odds2t: 30/30 parsed
2026-06-22 13:19:20,877 [INFO] scraper: odds2f: 15/15 parsed
2026-06-22 13:19:22,092 [INFO] scraper: odds_win: 6/6 parsed
2026-06-22 13:19:22,092 [INFO] scraper: fetch_race 17/6: boats=6 odds=191/191
2026-06-22 13:19:22,103 [INFO] predictor: CALIBRATION_MODE=on
2026-06-22 13:19:22,104 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-22 13:19:22,111 [INFO] run_cycle: fetched 17/6 [final]: 156 combos
2026-06-22 13:19:26,123 [INFO] scraper: odds3t: 120/120 parsed
2026-06-22 13:19:27,293 [INFO] scraper: odds3f: 20/20 parsed
2026-06-22 13:19:28,965 [INFO] scraper: odds2t: 22/30 parsed
2026-06-22 13:19:28,967 [INFO] scraper: odds2f: 13/15 parsed
2026-06-22 13:19:30,096 [INFO] scraper: odds_win: 3/6 parsed
2026-06-22 13:19:30,096 [INFO] scraper: fetch_race 08/7: boats=6 odds=178/191
2026-06-22 13:19:30,099 [INFO] predictor: CALIBRATION_MODE=on
2026-06-22 13:19:30,099 [INFO] predictor: combos: {'win': 3, '2t': 22, '3t': 120}
2026-06-22 13:19:30,102 [INFO] run_cycle: fetched 08/7 [scan]: 145 combos
2026-06-22 13:19:32,678 [WARNING] scraper: beforeinfo parse failed: jcd=23 rno=11
2026-06-22 13:19:32,678 [WARNING] run_cycle: fetch None: 23/11
2026-06-22 13:19:32,678 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 54
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 54
  }
]
```

## Phase別通知記録 (24h)
{'final': 19, 'result': 15, 'scan': 20}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 93
  FINAL_MISSING: 42
  CIRCUIT_BREAKER_NO_ACTION: 36
  CIRCUIT_BREAKER_TRIP: 30
  STRATEGY_CI_FAIL: 17
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_SCAN_FINAL_RATIO: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 10 | 10,800 | 8,010 | -2,790 | 0.742 |
| S01_NAKAANA1 | 37 | 7 | 7,400 | 3,100 | -4,300 | 0.419 |
| S02_TETSUBAN | 14 | 5 | 2,800 | 1,920 | -880 | 0.686 |

## 直近アラート (24h・新しい順)
```
[13:19:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1262}
[13:18:17] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1259}
[13:17:41] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1258}
[13:15:17] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1272}
[13:14:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1277}
[13:13:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1275}
[13:12:42] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1270}
[13:11:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1268}
[13:10:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1265}
[13:09:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1254}
```

## 本日残レース: 104件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 64件 締切済
- 通知発射: scan=4 nid / final=4 nid / result=2 nid
- predictions: 3 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 222R | win | 1 | 0.3177 | 26.2 | 8.32 | 300 | scan=4.5 drift=+482.2% | 12:58:23 |
| S01_NAKAANA1 | 084R | win | 1 | 0.4111 | 4.1 | 1.69 | 200 | scan=- drift=- | 11:54:20 |
| S01_NAKAANA1 | 106R | win | 1 | 0.5714 | 3.7 | 2.11 | 200 | scan=3.5 drift=+5.7% | 10:41:22 |
| S01_NAKAANA1 | 203R | win | 1 | 0.4989 | 3.8 | 1.90 | 200 | scan=3.0 drift=+26.7% | 18:31:21 |
| S00 | 194R | win | 1 | 0.5891 | 21.7 | 12.78 | 300 | scan=20.2 drift=+7.4% | 16:54:22 |
| S00 | 154R | win | 1 | 0.5174 | 6.6 | 3.41 | 300 | scan=7.5 drift=-12.0% | 16:42:21 |
| S00 | 192R | win | 1 | 0.5735 | 5.2 | 2.98 | 300 | scan=- drift=- | 15:49:44 |
| S01_NAKAANA1 | 0810R | win | 1 | 0.4111 | 4.5 | 1.85 | 200 | scan=4.5 drift=+0.0% | 14:55:23 |
| S00 | 0810R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=4.5 drift=+0.0% | 14:55:22 |
| S00 | 045R | win | 1 | 0.1760 | 4.1 | 0.72 | 300 | scan=5.5 drift=-25.5% | 13:52:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 52 | +4.7% | -61.4% | +482.2% | 19 | 8 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 364.4s |
| **Latency** (scan→final max) | 598.6s |
| **Traffic** (notifications 24h) | 54 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 366 | 0.4745 | 0.2869 | +0.1876 | 🟡+40% | 0.2425 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 147 | 0.4257 | 0.2585 | 0.2247 | 🔴-0.17 | 0.697 |
| S01_NAKAANA1 | win | 141 | 0.4902 | 0.2766 | 0.2462 | 🔴-0.23 | 0.733 |
| S02_TETSUBAN | win | 78 | 0.5380 | 0.3590 | 0.2692 | 🔴-0.17 | 0.608 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0816 | 0.0000 | 🔴+0.0816 |
| 0.15-0.20 | 7 | 0.1808 | 0.4286 | 🔴-0.2478 |
| 0.20-0.30 | 9 | 0.2241 | 0.1111 | 🔴+0.1130 |
| 0.30-0.50 | 123 | 0.4254 | 0.2439 | 🔴+0.1815 |
| 0.50+ | 216 | 0.5425 | 0.3241 | 🔴+0.2184 |

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
_auto-generated by claude_snapshot.py at 2026-06-22T13:20:01.437494+09:00_