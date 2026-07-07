# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-07T13:10:00.410561+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×29 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×51 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×29 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×12  [2026-07-07T13:04:38]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×6  [2026-07-07T13:04:38]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×30  [2026-07-07T12:28:15]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×56  [2026-07-07T12:04:33]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×13  [2026-07-07T12:02:00]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-07T12:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-07T12:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×27  [2026-07-07T11:00:43]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-07T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-07T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=165<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-07T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=14 pred=0.2291 actual=0.0714 gap=+0.1577`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-07T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1746 actual=0.4286 gap=-0.2540`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-07T06:00:10]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=29 hit%=37.9% ROI=1.08 (コスト 7,100/回収 7,670)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-07T06:00:10]
- key: `DRIFT_BUCKET|drift ≥+30%: n=28 hit%=21.4% ROI=0.51 (コスト 7,900/回収 3,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-07-07T06:00:10]
- key: `ROI_STAT|S00: n=165 hit%=29.7% hit_CI[Bonf]=[20.6,40.7]% ROI=0.80 ROI_boot95=[0.59,1.02]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-07T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=151 hit%=32.5% hit_CI[Bonf]=[22.6,44.1]% ROI=0.88 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-07T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=151<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-07T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=39.7% hit_CI[Bonf]=[25.5,56.0]% ROI=0.69 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-07-07T06:00:10]
- key: `ORPHAN_SCAN|164 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-07T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=36.4% ROI=1.05 (コスト 9,600/回収 10,050)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 7.02MB / last modified 2026-07-07T13:09:34.780327+09:00

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
_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-07 13:09:05,576 [INFO] predictor: Models loaded OK
2026-07-07 13:09:16,989 [INFO] scraper: odds3t: 120/120 parsed
2026-07-07 13:09:18,121 [INFO] scraper: odds3f: 20/20 parsed
2026-07-07 13:09:19,246 [INFO] scraper: odds2t: 30/30 parsed
2026-07-07 13:09:19,247 [INFO] scraper: odds2f: 15/15 parsed
2026-07-07 13:09:20,359 [INFO] scraper: odds_win: 6/6 parsed
2026-07-07 13:09:20,360 [INFO] scraper: fetch_race 02/6: boats=6 odds=191/191
2026-07-07 13:09:20,371 [INFO] predictor: CALIBRATION_MODE=on
2026-07-07 13:09:20,371 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-07 13:09:20,379 [INFO] run_cycle: fetched 02/6 [final]: 156 combos
2026-07-07 13:09:23,835 [INFO] scraper: odds3t: 120/120 parsed
2026-07-07 13:09:24,911 [INFO] scraper: odds3f: 20/20 parsed
2026-07-07 13:09:26,024 [INFO] scraper: odds2t: 30/30 parsed
2026-07-07 13:09:26,025 [INFO] scraper: odds2f: 15/15 parsed
2026-07-07 13:09:27,140 [INFO] scraper: odds_win: 6/6 parsed
2026-07-07 13:09:27,140 [INFO] scraper: fetch_race 11/6: boats=6 odds=191/191
2026-07-07 13:09:27,149 [INFO] predictor: CALIBRATION_MODE=on
2026-07-07 13:09:27,151 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-07 13:09:27,159 [INFO] run_cycle: fetched 11/6 [scan]: 156 combos
2026-07-07 13:09:30,714 [INFO] scraper: odds3t: 120/120 parsed
2026-07-07 13:09:31,805 [INFO] scraper: odds3f: 20/20 parsed
2026-07-07 13:09:32,963 [INFO] scraper: odds2t: 30/30 parsed
2026-07-07 13:09:32,964 [INFO] scraper: odds2f: 15/15 parsed
2026-07-07 13:09:34,045 [INFO] scraper: odds_win: 4/6 parsed
2026-07-07 13:09:34,045 [INFO] scraper: fetch_race 10/11: boats=6 odds=189/191
2026-07-07 13:09:34,056 [INFO] predictor: CALIBRATION_MODE=on
2026-07-07 13:09:34,057 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-07-07 13:09:34,064 [INFO] run_cycle: fetched 10/11 [scan]: 154 combos
2026-07-07 13:09:34,183 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 23, 'result': 15, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 101
  FINAL_MISSING: 51
  CIRCUIT_BREAKER_NO_ACTION: 33
  CIRCUIT_BREAKER_TRIP: 29
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 7
  ANOMALY_BET_VOLUME_DROP: 4
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 33 | 11 | 9,900 | 7,440 | -2,460 | 0.752 |
| S01_NAKAANA1 | 36 | 9 | 7,200 | 5,160 | -2,040 | 0.717 |
| S02_TETSUBAN | 25 | 13 | 5,000 | 4,980 | -20 | 0.996 |

## 直近アラート (24h・新しい順)
```
[13:04:38] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:04:38] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[13:04:38] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[12:58:35] CIRCUIT_BREAKER_TRIP: {"cost": 10200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 7020, "roi_7d": 0.688, "sid": "S00"}
[12:55:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 943}
[12:53:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 946}
[12:52:47] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 937}
[12:51:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 931}
[12:50:44] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 921}
[12:49:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 948}
```

## 本日残レース: 95件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 49件 締切済
- 通知発射: scan=10 nid / final=11 nid / result=4 nid
- predictions: 4 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 053R | win | 1 | 0.4989 | 9.9 | 4.94 | 300 | scan=19.5 drift=-49.2% | 12:30:26 |
| S01_NAKAANA1 | 109R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=- drift=- | 12:15:23 |
| S01_NAKAANA1 | 023R | win | 1 | 0.4111 | 4.6 | 1.89 | 200 | scan=- drift=- | 11:39:21 |
| S00 | 187R | win | 1 | 0.1149 | 4.1 | 0.47 | 300 | scan=- drift=- | 11:28:22 |
| S01_NAKAANA1 | 017R | win | 1 | 0.5891 | 4.1 | 2.42 | 200 | scan=4.1 drift=+0.0% | 18:18:22 |
| S00 | 017R | win | 1 | 0.5891 | 4.1 | 2.42 | 300 | scan=4.1 drift=+0.0% | 18:18:21 |
| S02_TETSUBAN | 076R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=2.1 drift=+0.0% | 18:01:20 |
| S01_NAKAANA1 | 124R | win | 1 | 0.5123 | 3.4 | 1.74 | 200 | scan=3.2 drift=+6.2% | 16:58:21 |
| S01_NAKAANA1 | 012R | win | 1 | 0.3177 | 3.0 | 0.95 | 200 | scan=- drift=- | 15:56:33 |
| S01_NAKAANA1 | 047R | win | 1 | 0.4989 | 4.3 | 2.15 | 200 | scan=4.2 drift=+2.4% | 14:57:24 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 50 | +1.8% | -52.8% | +200.0% | 15 | 4 | 28 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 460.4s |
| **Latency** (scan→final max) | 648.2s |
| **Traffic** (notifications 24h) | 64 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 389 | 0.4775 | 0.3342 | +0.1433 | 🟡+30% | 0.2365 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 164 | 0.4401 | 0.3049 | 0.2210 | 🔴-0.04 | 0.81 |
| S01_NAKAANA1 | win | 149 | 0.4865 | 0.3356 | 0.2409 | 🔴-0.08 | 0.918 |
| S02_TETSUBAN | win | 76 | 0.5402 | 0.3947 | 0.2611 | 🔴-0.09 | 0.691 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1746 | 0.4286 | 🔴-0.2540 |
| 0.20-0.30 | 14 | 0.2291 | 0.0714 | 🔴+0.1577 |
| 0.30-0.50 | 137 | 0.4198 | 0.3066 | 🔴+0.1132 |
| 0.50+ | 227 | 0.5438 | 0.3700 | 🔴+0.1737 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 62 | 0.755 |
| win | <5.0 | ✅learned | 124 | 0.716 |
| win | <10.0 | ✅learned | 66 | 0.474 |
| win | <20.0 | ✅learned | 19 | 0.212 |
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
_auto-generated by claude_snapshot.py at 2026-07-07T13:10:00.410561+09:00_