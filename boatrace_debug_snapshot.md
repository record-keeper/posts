# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-14T15:20:01.323611+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×62 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×5 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×2  [2026-07-14T15:18:37]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×18  [2026-07-14T15:02:38]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×18  [2026-07-14T15:02:38]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-14T14:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×46  [2026-07-14T14:15:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×14  [2026-07-14T11:55:23]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-07-14T10:00:40]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-14T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-14T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=69<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-14T06:00:06]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=29 pred=0.3244 actual=0.1034 gap=+0.2210`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-14T06:00:06]
- key: `ROI_STAT|S00: n=176 hit%=29.5% hit_CI[Bonf]=[20.7,40.2]% ROI=0.76 ROI_boot95=[0.57,0.97]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-14T06:00:06]
- key: `ROI_STAT|S01_NAKAANA1: n=156 hit%=30.8% hit_CI[Bonf]=[21.3,42.2]% ROI=0.81 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-14T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=156<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-14T06:00:06]
- key: `ROI_STAT|S02_TETSUBAN: n=69 hit%=43.5% hit_CI[Bonf]=[27.9,60.5]% ROI=0.86 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-07-14T06:00:06]
- key: `ORPHAN_SCAN|173 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-14T06:00:06]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=33.3% ROI=0.86 (コスト 9,700/回収 8,340)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-14T06:00:06]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=46 hit%=32.6% ROI=0.77 (コスト 11,200/回収 8,580)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-14T06:00:06]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=88 hit%=33.0% ROI=0.90 (コスト 20,200/回収 18,230)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-14T06:00:06]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=37 hit%=32.4% ROI=0.75 (コスト 9,100/回収 6,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-14T06:00:06]
- key: `DRIFT_BUCKET|drift ≥+30%: n=31 hit%=22.6% ROI=0.45 (コスト 8,600/回収 3,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 7.69MB / last modified 2026-07-14T15:19:26.654167+09:00

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
ed
2026-07-14 15:18:37,415 [INFO] scraper: fetch_race 15/1: boats=6 odds=189/191
2026-07-14 15:18:37,417 [INFO] predictor: CALIBRATION_MODE=on
2026-07-14 15:18:37,417 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-07-14 15:18:37,421 [INFO] run_cycle: fetched 15/1 [scan]: 154 combos
2026-07-14 15:18:37,515 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-14 15:19:04,099 [INFO] run_cycle: === run_cycle 15:19:04 ===
2026-07-14 15:19:04,100 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-14 15:19:04,100 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-14 15:19:04,126 [INFO] predictor: Models loaded OK
2026-07-14 15:19:15,549 [INFO] scraper: odds3t: 120/120 parsed
2026-07-14 15:19:16,706 [INFO] scraper: odds3f: 20/20 parsed
2026-07-14 15:19:17,927 [INFO] scraper: odds2t: 30/30 parsed
2026-07-14 15:19:17,928 [INFO] scraper: odds2f: 14/15 parsed
2026-07-14 15:19:19,042 [INFO] scraper: odds_win: 6/6 parsed
2026-07-14 15:19:19,042 [INFO] scraper: fetch_race 03/10: boats=6 odds=190/191
2026-07-14 15:19:19,045 [INFO] predictor: CALIBRATION_MODE=on
2026-07-14 15:19:19,045 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-14 15:19:19,049 [INFO] run_cycle: fetched 03/10 [final]: 156 combos
2026-07-14 15:19:22,773 [INFO] scraper: odds3t: 120/120 parsed
2026-07-14 15:19:23,895 [INFO] scraper: odds3f: 20/20 parsed
2026-07-14 15:19:25,168 [INFO] scraper: odds2t: 30/30 parsed
2026-07-14 15:19:25,169 [INFO] scraper: odds2f: 15/15 parsed
2026-07-14 15:19:26,402 [INFO] scraper: odds_win: 2/6 parsed
2026-07-14 15:19:26,402 [INFO] scraper: fetch_race 04/8: boats=6 odds=187/191
2026-07-14 15:19:26,404 [INFO] predictor: CALIBRATION_MODE=on
2026-07-14 15:19:26,404 [INFO] predictor: combos: {'win': 2, '2t': 30, '3t': 120}
2026-07-14 15:19:26,408 [INFO] run_cycle: fetched 04/8 [scan]: 152 combos
2026-07-14 15:19:26,500 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 41
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 41
  }
]
```

## Phase別通知記録 (24h)
{'final': 16, 'result': 10, 'scan': 15}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 71
  FINAL_MISSING: 62
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 5
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 47 | 16 | 14,100 | 13,590 | -510 | 0.964 |
| S01_NAKAANA1 | 36 | 10 | 7,200 | 4,760 | -2,440 | 0.661 |
| S02_TETSUBAN | 18 | 7 | 3,600 | 3,400 | -200 | 0.944 |

## 直近アラート (24h・新しい順)
```
[15:04:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 938}
[15:03:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 920}
[15:02:37] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:02:37] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[15:02:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 911}
[15:01:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 929}
[14:59:18] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 927}
[14:58:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 922}
[14:57:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 932}
[14:56:18] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 931}
```

## 本日残レース: 72件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 84件 締切済
- 通知発射: scan=11 nid / final=10 nid / result=5 nid
- predictions: 5 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 097R | win | 1 | 0.1371 | 48.0 | 6.58 | 300 | scan=18.7 drift=+156.7% | 13:38:26 |
| S00 | 054R | win | 1 | 0.4111 | 5.7 | 2.34 | 300 | scan=- drift=- | 13:01:30 |
| S01_NAKAANA1 | 053R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=3.0 drift=+0.0% | 12:31:19 |
| S01_NAKAANA1 | 063R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=4.5 drift=-33.3% | 12:23:19 |
| S02_TETSUBAN | 218R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=2.1 drift=+0.0% | 11:45:18 |
| S02_TETSUBAN | 078R | win | 1 | 0.5174 | 2.7 | 1.40 | 200 | scan=2.5 drift=+8.0% | 18:39:19 |
| S01_NAKAANA1 | 073R | win | 1 | 0.4111 | 4.7 | 1.93 | 200 | scan=4.2 drift=+11.9% | 16:12:20 |
| S00 | 073R | win | 1 | 0.4111 | 4.7 | 1.93 | 300 | scan=4.2 drift=+11.9% | 16:12:20 |
| S02_TETSUBAN | 072R | win | 1 | 0.5735 | 2.1 | 1.20 | 200 | scan=- drift=- | 15:44:29 |
| S01_NAKAANA1 | 0310R | win | 1 | 0.5334 | 3.1 | 1.65 | 200 | scan=3.0 drift=+3.3% | 15:19:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 57 | +23.8% | -73.3% | +533.3% | 15 | 5 | 40 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 404.5s |
| **Latency** (scan→final max) | 605.1s |
| **Traffic** (notifications 24h) | 41 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 394 | 0.4683 | 0.3147 | +0.1536 | 🟡+33% | 0.2354 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 173 | 0.4290 | 0.2890 | 0.2236 | 🔴-0.09 | 0.738 |
| S01_NAKAANA1 | win | 153 | 0.4792 | 0.2941 | 0.2368 | 🔴-0.14 | 0.735 |
| S02_TETSUBAN | win | 68 | 0.5440 | 0.4265 | 0.2626 | 🔴-0.07 | 0.85 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1777 | 0.5714 | 🔴-0.3938 |
| 0.20-0.30 | 16 | 0.2282 | 0.1875 | ✅+0.0407 |
| 0.30-0.50 | 146 | 0.4161 | 0.2740 | 🔴+0.1421 |
| 0.50+ | 218 | 0.5420 | 0.3532 | 🔴+0.1888 |

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
_auto-generated by claude_snapshot.py at 2026-07-14T15:20:01.323611+09:00_