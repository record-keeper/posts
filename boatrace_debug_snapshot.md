# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-30T11:50:01.379584+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×34 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×101 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×34 (24h)
- 🔴 PSI_DRIFT_DETECTED×30 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×4  [2026-09-30T11:46:40]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×92  [2026-09-30T11:04:42]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×92  [2026-09-30T11:04:42]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×46  [2026-09-30T11:04:42]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×46  [2026-09-30T11:04:42]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×50  [2026-09-30T11:00:49]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-09-30T10:30:06]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-09-30T10:30:06]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ORPHAN_SCAN  ×1  [2026-09-30T06:00:36]
- key: `ORPHAN_SCAN|175 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-30T06:00:36]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-30T06:00:36]
- key: `INSUFFICIENT_SAMPLE|S00: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-30T06:00:36]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=165<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-30T06:00:36]
- key: `ROI_STAT|S00: n=164 hit%=21.3% hit_CI[Bonf]=[13.6,31.8]% ROI=0.64 ROI_boot95=[0.41,0.89]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-30T06:00:36]
- key: `ROI_STAT|S01_NAKAANA1: n=165 hit%=23.0% hit_CI[Bonf]=[15.0,33.6]% ROI=0.68 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-30T06:00:36]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=47.4% hit_CI[Bonf]=[32.2,63.2]% ROI=0.81 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-30T06:00:36]
- key: `DRIFT_BUCKET|drift ≤-30%: n=28 hit%=35.7% ROI=1.04 (コスト 7,800/回収 8,130)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-30T06:00:36]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=44 hit%=25.0% ROI=0.67 (コスト 10,200/回収 6,790)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-30T06:00:36]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=92 hit%=23.9% ROI=0.69 (コスト 21,400/回収 14,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-30T06:00:36]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=42 hit%=26.2% ROI=0.48 (コスト 9,300/回収 4,460)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-30T06:00:36]
- key: `DRIFT_BUCKET|drift ≥+30%: n=40 hit%=7.5% ROI=0.14 (コスト 10,700/回収 1,540)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 14.55MB / last modified 2026-09-30T11:49:06.347294+09:00

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
ds3t: 120/120 parsed
2026-09-30 11:48:17,537 [INFO] scraper: odds3f: 20/20 parsed
2026-09-30 11:48:18,645 [INFO] scraper: odds2t: 30/30 parsed
2026-09-30 11:48:18,647 [INFO] scraper: odds2f: 15/15 parsed
2026-09-30 11:48:19,753 [INFO] scraper: odds_win: 4/6 parsed
2026-09-30 11:48:19,753 [INFO] scraper: fetch_race 04/3: boats=6 odds=189/191
2026-09-30 11:48:19,756 [INFO] predictor: CALIBRATION_MODE=on
2026-09-30 11:48:19,756 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-09-30 11:48:19,760 [INFO] run_cycle: fetched 04/3 [scan]: 154 combos
2026-09-30 11:48:23,247 [INFO] scraper: odds3t: 120/120 parsed
2026-09-30 11:48:24,346 [INFO] scraper: odds3f: 20/20 parsed
2026-09-30 11:48:25,474 [INFO] scraper: odds2t: 21/30 parsed
2026-09-30 11:48:25,475 [INFO] scraper: odds2f: 14/15 parsed
2026-09-30 11:48:26,591 [INFO] scraper: odds_win: 3/6 parsed
2026-09-30 11:48:26,695 [INFO] scraper: fetch_race 09/4: boats=6 odds=178/191
2026-09-30 11:48:26,699 [INFO] predictor: CALIBRATION_MODE=on
2026-09-30 11:48:26,699 [INFO] predictor: combos: {'win': 3, '2t': 21, '3t': 120}
2026-09-30 11:48:26,703 [INFO] run_cycle: fetched 09/4 [scan]: 144 combos
2026-09-30 11:48:27,003 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-30 11:49:05,018 [INFO] run_cycle: === run_cycle 11:49:05 ===
2026-09-30 11:49:05,018 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-30 11:49:05,018 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-30 11:49:05,083 [INFO] predictor: Models loaded OK
2026-09-30 11:49:05,528 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-30 11:50:07,017 [INFO] run_cycle: === run_cycle 11:50:07 ===
2026-09-30 11:50:07,017 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-30 11:50:07,017 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-30 11:50:07,110 [INFO] predictor: Models loaded OK

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
    "c": 75
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 75
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 21, 'scan': 29}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 111
  FINAL_MISSING: 101
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 34
  PSI_DRIFT_DETECTED: 30
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 13
  ANOMALY_SCAN_FINAL_RATIO: 6
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 39 | 7 | 11,700 | 5,700 | -6,000 | 0.487 |
| S01_NAKAANA1 | 39 | 11 | 7,800 | 5,360 | -2,440 | 0.687 |
| S02_TETSUBAN | 25 | 14 | 5,000 | 4,900 | -100 | 0.98 |

## 直近アラート (24h・新しい順)
```
[11:47:21] CIRCUIT_BREAKER_TRIP: {"cost": 11700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 39, "payout": 5700, "roi_7d": 0.487, "sid": "S00"}
[11:47:21] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 305, "n_recent": 103, "psi": 0.379}
[11:46:39] FINAL_MISSING: {"deadline": "2026-09-30T10:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026093014051016", "sid": "S00"}
[11:46:39] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.243, "baseline_mean": 0.814, "baseline_stdev": 0.095, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.571, "today_scan_count": 7, "z_score": -2.55}
[11:38:34] CIRCUIT_BREAKER_TRIP: {"cost": 12000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 5700, "roi_7d": 0.475, "sid": "S00"}
[11:38:34] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 304, "n_recent": 104, "psi": 0.379}
[11:25:44] CIRCUIT_BREAKER_TRIP: {"cost": 12300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 41, "payout": 5700, "roi_7d": 0.463, "sid": "S00"}
[11:21:40] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.214, "baseline_mean": 0.814, "baseline_stdev": 0.095, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.6, "today_scan_count": 5, "z_score": -2.25}
[11:20:24] FINAL_MISSING: {"deadline": "2026-09-30T09:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026093014040950", "sid": "S00"}
[11:13:45] CIRCUIT_BREAKER_TRIP: {"cost": 7800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 39, "payout": 5360, "roi_7d": 0.687, "sid": "S01_NAKAANA1"}
```

## 本日残レース: 113件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 31件 締切済
- 通知発射: scan=7 nid / final=4 nid / result=2 nid
- predictions: 2 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 041R | win | 1 | 0.3177 | 6.5 | 2.07 | 300 | scan=20.2 drift=-67.8% | 10:53:20 |
| S01_NAKAANA1 | 145R | win | 1 | 0.4978 | 3.9 | 1.94 | 200 | scan=4.0 drift=-2.5% | 10:13:31 |
| S02_TETSUBAN | 078R | win | 1 | 0.5334 | 2.2 | 1.17 | 200 | scan=2.0 drift=+10.0% | 18:38:32 |
| S02_TETSUBAN | 074R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=- drift=- | 16:39:30 |
| S00 | 154R | win | 1 | 0.4111 | 6.5 | 2.67 | 300 | scan=- drift=- | 16:31:20 |
| S01_NAKAANA1 | 153R | win | 1 | 0.3177 | 4.3 | 1.37 | 200 | scan=4.7 drift=-8.5% | 16:03:32 |
| S01_NAKAANA1 | 0211R | win | 1 | 0.4111 | 3.4 | 1.40 | 200 | scan=3.0 drift=+13.3% | 15:52:31 |
| S02_TETSUBAN | 168R | win | 1 | 0.4989 | 2.7 | 1.35 | 200 | scan=2.3 drift=+17.4% | 14:35:31 |
| S01_NAKAANA1 | 056R | win | 1 | 0.4111 | 3.3 | 1.36 | 200 | scan=3.9 drift=-15.4% | 13:30:23 |
| S01_NAKAANA1 | 026R | win | 1 | 0.5891 | 4.2 | 2.47 | 200 | scan=3.4 drift=+23.5% | 13:11:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 66 | +6.8% | -72.2% | +357.1% | 21 | 8 | 41 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 432.7s |
| **Latency** (scan→final max) | 606.1s |
| **Traffic** (notifications 24h) | 75 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 408 | 0.4797 | 0.2721 | +0.2076 | 🟡+43% | 0.2457 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 165 | 0.4488 | 0.2182 | 0.2385 | 🔴-0.40 | 0.658 |
| S01_NAKAANA1 | win | 165 | 0.4890 | 0.2303 | 0.2481 | 🔴-0.40 | 0.676 |
| S02_TETSUBAN | win | 78 | 0.5253 | 0.4744 | 0.2556 | 🔴-0.03 | 0.809 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 155 | 0.4137 | 0.2323 | 🔴+0.1815 |
| 0.50+ | 238 | 0.5445 | 0.3025 | 🔴+0.2420 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 163 | 0.771 |
| win | <5.0 | ✅learned | 277 | 0.752 |
| win | <10.0 | ✅learned | 127 | 0.462 |
| win | <20.0 | ✅learned | 34 | 0.237 |
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
_auto-generated by claude_snapshot.py at 2026-09-30T11:50:01.379584+09:00_