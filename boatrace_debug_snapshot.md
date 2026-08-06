# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-06T16:50:01.748129+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×37 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-06T16:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-06T16:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×27  [2026-08-06T16:23:20]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×88  [2026-08-06T16:05:26]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×44  [2026-08-06T16:05:26]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×48  [2026-08-06T16:01:21]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×16  [2026-08-06T11:42:36]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-06T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=67<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-06T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S00: n=178<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-06T06:00:21]
- key: `ORPHAN_SCAN|170 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-06T06:00:21]
- key: `DRIFT_BUCKET|drift ≥+30%: n=40 hit%=25.0% ROI=0.88 (コスト 11,100/回収 9,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-06T06:00:21]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2244 actual=0.4000 gap=-0.1756`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-06T06:00:21]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=12 pred=0.1235 actual=0.1667 gap=-0.0432`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-06T06:00:21]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=10 pred=0.1823 actual=0.2000 gap=-0.0177`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-06T06:00:21]
- key: `ROI_STAT|S00: n=178 hit%=25.8% hit_CI[Bonf]=[17.6,36.2]% ROI=0.72 ROI_boot95=[0.51,0.96]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-06T06:00:21]
- key: `ROI_STAT|S01_NAKAANA1: n=154 hit%=24.7% hit_CI[Bonf]=[16.1,35.8]% ROI=0.73 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-06T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=154<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-06T06:00:21]
- key: `ROI_STAT|S02_TETSUBAN: n=67 hit%=50.7% hit_CI[Bonf]=[34.0,67.3]% ROI=0.97 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-06T06:00:21]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=22.9% ROI=0.65 (コスト 10,300/回収 6,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-06T06:00:21]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=34 hit%=35.3% ROI=0.85 (コスト 8,600/回収 7,320)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 9.55MB / last modified 2026-08-06T16:49:03.670223+09:00

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
=5000
2026-08-06 16:48:04,256 [INFO] predictor: Models loaded OK
2026-08-06 16:48:15,324 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=4&jcd=19&hd=20260806: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-06 16:48:26,776 [INFO] scraper: odds3t: 120/120 parsed
2026-08-06 16:48:27,901 [INFO] scraper: odds3f: 20/20 parsed
2026-08-06 16:48:28,978 [INFO] scraper: odds2t: 30/30 parsed
2026-08-06 16:48:28,979 [INFO] scraper: odds2f: 14/15 parsed
2026-08-06 16:48:30,088 [INFO] scraper: odds_win: 4/6 parsed
2026-08-06 16:48:30,088 [INFO] scraper: fetch_race 19/4: boats=6 odds=188/191
2026-08-06 16:48:30,092 [INFO] predictor: CALIBRATION_MODE=on
2026-08-06 16:48:30,092 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-08-06 16:48:30,096 [INFO] run_cycle: fetched 19/4 [final]: 154 combos
2026-08-06 16:48:33,582 [INFO] scraper: odds3t: 120/120 parsed
2026-08-06 16:48:34,651 [INFO] scraper: odds3f: 20/20 parsed
2026-08-06 16:48:35,761 [INFO] scraper: odds2t: 30/30 parsed
2026-08-06 16:48:35,762 [INFO] scraper: odds2f: 14/15 parsed
2026-08-06 16:48:36,831 [INFO] scraper: odds_win: 3/6 parsed
2026-08-06 16:48:36,831 [INFO] scraper: fetch_race 12/5: boats=6 odds=187/191
2026-08-06 16:48:36,833 [INFO] predictor: CALIBRATION_MODE=on
2026-08-06 16:48:36,833 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-08-06 16:48:36,837 [INFO] run_cycle: fetched 12/5 [scan]: 153 combos
2026-08-06 16:48:36,945 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-06 16:49:03,402 [INFO] run_cycle: === run_cycle 16:49:03 ===
2026-08-06 16:49:03,402 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-06 16:49:03,402 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-06 16:49:03,452 [INFO] predictor: Models loaded OK
2026-08-06 16:49:03,556 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 35
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 35
  }
]
```

## Phase別通知記録 (24h)
{'final': 13, 'result': 5, 'scan': 17}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 171
  FINAL_MISSING: 37
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 34 | 9 | 10,200 | 9,030 | -1,170 | 0.885 |
| S01_NAKAANA1 | 32 | 8 | 6,400 | 5,040 | -1,360 | 0.787 |
| S02_TETSUBAN | 9 | 5 | 1,800 | 1,500 | -300 | 0.833 |

## 直近アラート (24h・新しい順)
```
[16:49:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 937}
[16:48:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 933}
[16:47:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 931}
[16:46:38] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 935}
[16:45:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 938}
[16:44:18] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 937}
[16:43:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 957}
[16:40:40] FINAL_MISSING: {"deadline": "2026-08-06T16:10:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080612031610", "sid": "S00"}
[16:40:40] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 974}
[16:39:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 973}
```

## 本日残レース: 26件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 120件 登録 / 94件 締切済
- 通知発射: scan=11 nid / final=11 nid / result=5 nid
- predictions: 5 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 1410R | win | 1 | 0.4989 | 3.5 | 1.75 | 200 | scan=3.5 drift=+0.0% | 13:15:19 |
| S01_NAKAANA1 | 026R | win | 1 | 0.5123 | 4.5 | 2.31 | 200 | scan=- drift=- | 13:11:19 |
| S00 | 173R | win | 1 | 0.4111 | 29.5 | 12.13 | 300 | scan=42.7 drift=-30.9% | 11:47:30 |
| S01_NAKAANA1 | 147R | win | 1 | 0.5735 | 3.2 | 1.84 | 200 | scan=3.3 drift=-3.0% | 11:32:43 |
| S01_NAKAANA1 | 146R | win | 1 | 0.5123 | 3.2 | 1.64 | 200 | scan=- drift=- | 10:57:31 |
| S00 | 098R | win | 1 | 0.3177 | 10.5 | 3.34 | 300 | scan=18.0 drift=-41.7% | 13:58:19 |
| S00 | 045R | win | 1 | 0.3177 | 9.5 | 3.02 | 300 | scan=10.5 drift=-9.5% | 13:52:19 |
| S01_NAKAANA1 | 055R | win | 1 | 0.5891 | 4.6 | 2.71 | 200 | scan=- drift=- | 13:28:18 |
| S01_NAKAANA1 | 149R | win | 1 | 0.5891 | 3.5 | 2.06 | 200 | scan=3.9 drift=-10.3% | 12:35:45 |
| S00 | 053R | win | 1 | 0.5476 | 4.2 | 2.30 | 300 | scan=- drift=- | 12:29:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 46 | -4.9% | -73.3% | +107.5% | 17 | 12 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 534.1s |
| **Latency** (scan→final max) | 618.7s |
| **Traffic** (notifications 24h) | 35 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 396 | 0.4614 | 0.2904 | +0.1710 | 🟡+37% | 0.2354 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 176 | 0.4166 | 0.2500 | 0.2245 | 🔴-0.20 | 0.71 |
| S01_NAKAANA1 | win | 154 | 0.4845 | 0.2468 | 0.2430 | 🔴-0.31 | 0.715 |
| S02_TETSUBAN | win | 66 | 0.5267 | 0.5000 | 0.2465 | ✅+0.01 | 0.948 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 11 | 0.1242 | 0.1818 | 🔴-0.0576 |
| 0.15-0.20 | 10 | 0.1823 | 0.2000 | ✅-0.0177 |
| 0.20-0.30 | 10 | 0.2244 | 0.4000 | 🔴-0.1756 |
| 0.30-0.50 | 151 | 0.4172 | 0.2119 | 🔴+0.2053 |
| 0.50+ | 211 | 0.5403 | 0.3555 | 🔴+0.1848 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 96 | 0.787 |
| win | <5.0 | ✅learned | 171 | 0.719 |
| win | <10.0 | ✅learned | 88 | 0.449 |
| win | <20.0 | ✅learned | 29 | 0.228 |
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
_auto-generated by claude_snapshot.py at 2026-08-06T16:50:01.748129+09:00_