# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-08T13:20:01.268030+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×47 (24h) → ログ/DB確認

### 検出された問題
- 🔴 PSI_DRIFT_DETECTED×47 (24h)
- 🟡 FINAL_MISSING×28 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×26 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×1  [2026-08-08T13:19:45]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×7  [2026-08-08T13:04:33]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×34  [2026-08-08T13:03:05]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×34  [2026-08-08T13:03:05]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×17  [2026-08-08T13:03:05]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-08T12:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-08T12:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×27  [2026-08-08T12:23:33]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×12  [2026-08-08T11:00:23]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-08T06:00:29]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-08T06:00:29]
- key: `ORPHAN_SCAN|171 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-08T06:00:29]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=161<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-08T06:00:29]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=10 pred=0.1823 actual=0.2000 gap=-0.0177`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-08T06:00:29]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=20.0% ROI=0.61 (コスト 10,300/回収 6,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-08-08T06:00:29]
- key: `ROI_STAT|S00: n=176 hit%=24.4% hit_CI[Bonf]=[16.4,34.8]% ROI=0.70 ROI_boot95=[0.50,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-08T06:00:29]
- key: `ROI_STAT|S01_NAKAANA1: n=161 hit%=24.8% hit_CI[Bonf]=[16.4,35.7]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-08T06:00:29]
- key: `ROI_STAT|S02_TETSUBAN: n=63 hit%=50.8% hit_CI[Bonf]=[33.6,67.8]% ROI=1.00 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-08T06:00:29]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=63<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-08T06:00:29]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=36 hit%=36.1% ROI=0.90 (コスト 9,000/回収 8,120)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-08T06:00:29]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=62 hit%=29.0% ROI=0.75 (コスト 14,700/回収 11,080)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 9.69MB / last modified 2026-08-08T13:19:45.689785+09:00

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
{'win': 4, '2t': 30, '3t': 120}
2026-08-08 13:19:29,833 [INFO] run_cycle: fetched 16/6 [final]: 154 combos
2026-08-08 13:19:29,869 [INFO] race_id: notif: nid=2026080816061322 sid=S00 phase=final rank=
2026-08-08 13:19:30,226 [INFO] notifier: Discord notify OK (status=204)
2026-08-08 13:19:30,712 [INFO] notifier: Discord notify OK (status=204)
2026-08-08 13:19:30,745 [INFO] run_cycle: RETREAT S00 児島6R
2026-08-08 13:19:30,753 [INFO] race_id: notif: nid=2026080816061322 sid=S02_TETSUBAN phase=final rank=B
2026-08-08 13:19:31,083 [INFO] notifier: Discord notify OK (status=204)
2026-08-08 13:19:31,591 [INFO] notifier: Discord notify OK (status=204)
2026-08-08 13:19:31,671 [INFO] run_cycle: FINAL S02_TETSUBAN 児島6R B
2026-08-08 13:19:35,074 [INFO] scraper: odds3t: 120/120 parsed
2026-08-08 13:19:36,193 [INFO] scraper: odds3f: 20/20 parsed
2026-08-08 13:19:37,272 [INFO] scraper: odds2t: 30/30 parsed
2026-08-08 13:19:37,273 [INFO] scraper: odds2f: 15/15 parsed
2026-08-08 13:19:38,388 [INFO] scraper: odds_win: 6/6 parsed
2026-08-08 13:19:38,388 [INFO] scraper: fetch_race 04/4: boats=6 odds=191/191
2026-08-08 13:19:38,390 [INFO] predictor: CALIBRATION_MODE=on
2026-08-08 13:19:38,391 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-08 13:19:38,394 [INFO] run_cycle: fetched 04/4 [scan]: 156 combos
2026-08-08 13:19:41,778 [INFO] scraper: odds3t: 120/120 parsed
2026-08-08 13:19:42,907 [INFO] scraper: odds3f: 19/20 parsed
2026-08-08 13:19:44,015 [INFO] scraper: odds2t: 29/30 parsed
2026-08-08 13:19:44,016 [INFO] scraper: odds2f: 14/15 parsed
2026-08-08 13:19:45,199 [INFO] scraper: odds_win: 3/6 parsed
2026-08-08 13:19:45,199 [INFO] scraper: fetch_race 09/7: boats=6 odds=185/191
2026-08-08 13:19:45,201 [INFO] predictor: CALIBRATION_MODE=on
2026-08-08 13:19:45,201 [INFO] predictor: combos: {'win': 3, '2t': 29, '3t': 120}
2026-08-08 13:19:45,205 [INFO] run_cycle: fetched 09/7 [scan]: 152 combos
2026-08-08 13:19:45,404 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 63
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 63
  }
]
```

## Phase別通知記録 (24h)
{'final': 26, 'result': 15, 'scan': 22}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 88
  PSI_DRIFT_DETECTED: 47
  CIRCUIT_BREAKER_NO_ACTION: 34
  FINAL_MISSING: 28
  CIRCUIT_BREAKER_TRIP: 26
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 6
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 28 | 6 | 8,400 | 5,040 | -3,360 | 0.6 |
| S01_NAKAANA1 | 35 | 7 | 7,000 | 3,920 | -3,080 | 0.56 |
| S02_TETSUBAN | 9 | 6 | 1,800 | 2,060 | +260 | 1.144 |

## 直近アラート (24h・新しい順)
```
[13:19:45] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1124}
[13:18:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1125}
[13:17:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1146}
[13:16:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1141}
[13:16:00] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1122}
[13:16:00] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.172, "baseline_mean": 0.839, "baseline_stdev": 0.078, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 9, "z_score": -2.2}
[13:14:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1104}
[13:04:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1068}
[13:03:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:03:04] CIRCUIT_BREAKER_TRIP: {"cost": 7000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 3920, "roi_7d": 0.56, "sid": "S01_NAKAANA1"}
```

## 本日残レース: 113件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 55件 締切済
- 通知発射: scan=9 nid / final=9 nid / result=5 nid
- predictions: 6 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 166R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=- drift=- | 13:19:30 |
| S00 | 025R | win | 1 | 0.5174 | 5.0 | 2.59 | 300 | scan=4.3 drift=+16.3% | 12:41:18 |
| S01_NAKAANA1 | 024R | win | 1 | 0.4111 | 4.2 | 1.73 | 200 | scan=- drift=- | 12:11:44 |
| S02_TETSUBAN | 163R | win | 1 | 0.5891 | 2.8 | 1.65 | 200 | scan=- drift=- | 11:47:18 |
| S00 | 162R | win | 1 | 0.4989 | 10.5 | 5.24 | 300 | scan=- drift=- | 11:12:19 |
| S00 | 021R | win | 1 | 0.5174 | 5.5 | 2.85 | 300 | scan=4.5 drift=+22.2% | 10:44:19 |
| S01_NAKAANA1 | 1510R | win | 1 | 0.4989 | 3.6 | 1.80 | 200 | scan=3.5 drift=+2.9% | 19:26:19 |
| S01_NAKAANA1 | 249R | win | 1 | 0.5123 | 4.7 | 2.41 | 200 | scan=- drift=- | 19:01:29 |
| S01_NAKAANA1 | 154R | win | 1 | 0.3177 | 4.5 | 1.43 | 200 | scan=3.1 drift=+45.2% | 16:37:19 |
| S00 | 124R | win | 1 | 0.2173 | 4.5 | 0.98 | 300 | scan=4.0 drift=+12.5% | 16:30:35 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 41 | -1.1% | -73.3% | +112.5% | 14 | 8 | 30 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 395.2s |
| **Latency** (scan→final max) | 592.3s |
| **Traffic** (notifications 24h) | 63 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 395 | 0.4588 | 0.2861 | +0.1727 | 🟡+38% | 0.2354 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 175 | 0.4118 | 0.2457 | 0.2223 | 🔴-0.20 | 0.703 |
| S01_NAKAANA1 | win | 157 | 0.4836 | 0.2420 | 0.2458 | 🔴-0.34 | 0.73 |
| S02_TETSUBAN | win | 63 | 0.5273 | 0.5079 | 0.2457 | ✅+0.02 | 0.995 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 12 | 0.1229 | 0.1667 | ✅-0.0438 |
| 0.15-0.20 | 10 | 0.1823 | 0.2000 | ✅-0.0177 |
| 0.20-0.30 | 11 | 0.2237 | 0.3636 | 🔴-0.1399 |
| 0.30-0.50 | 151 | 0.4165 | 0.2185 | 🔴+0.1979 |
| 0.50+ | 208 | 0.5399 | 0.3462 | 🔴+0.1938 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 97 | 0.791 |
| win | <5.0 | ✅learned | 173 | 0.725 |
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
_auto-generated by claude_snapshot.py at 2026-08-08T13:20:01.268030+09:00_