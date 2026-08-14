# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-14T11:30:01.737482+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×142 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×49 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-14T11:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-14T11:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×56  [2026-08-14T11:02:26]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×56  [2026-08-14T11:02:26]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×28  [2026-08-14T11:02:26]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×33  [2026-08-14T10:44:46]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-08-14T10:00:08]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-14T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S00: n=172<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-14T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=71<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-14T06:00:08]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=46 hit%=26.1% ROI=0.53 (コスト 10,600/回収 5,620)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-14T06:00:08]
- key: `DRIFT_BUCKET|drift ≥+30%: n=36 hit%=22.2% ROI=0.90 (コスト 10,000/回収 9,000)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-08-14T06:00:08]
- key: `ROI_STAT|S00: n=172 hit%=21.5% hit_CI[Bonf]=[13.9,31.8]% ROI=0.60 ROI_boot95=[0.41,0.83]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-14T06:00:08]
- key: `ROI_STAT|S01_NAKAANA1: n=169 hit%=20.7% hit_CI[Bonf]=[13.2,31.0]% ROI=0.61 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-14T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=169<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-14T06:00:08]
- key: `ROI_STAT|S02_TETSUBAN: n=71 hit%=53.5% hit_CI[Bonf]=[37.0,69.3]% ROI=0.90 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-08-14T06:00:08]
- key: `ORPHAN_SCAN|190 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-14T06:00:08]
- key: `DRIFT_BUCKET|drift ≤-30%: n=38 hit%=21.1% ROI=0.62 (コスト 11,000/回収 6,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-14T06:00:08]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=36 hit%=30.6% ROI=0.77 (コスト 8,800/回収 6,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-14T06:00:08]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=69 hit%=26.1% ROI=0.56 (コスト 16,100/回収 8,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-14T06:00:08]
- key: `CALIBRATION_LIVE|bt=win: n=412 pred=0.4671 actual=0.2670 error=+0.2001 (+43%) brier=0.2363 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.39MB / last modified 2026-08-14T11:30:05.066337+09:00

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
==
2026-08-14 11:29:03,420 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-14 11:29:03,420 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-14 11:29:03,469 [INFO] predictor: Models loaded OK
2026-08-14 11:29:16,007 [INFO] scraper: odds3t: 120/120 parsed
2026-08-14 11:29:17,154 [INFO] scraper: odds3f: 20/20 parsed
2026-08-14 11:29:18,306 [INFO] scraper: odds2t: 30/30 parsed
2026-08-14 11:29:18,308 [INFO] scraper: odds2f: 15/15 parsed
2026-08-14 11:29:19,406 [INFO] scraper: odds_win: 6/6 parsed
2026-08-14 11:29:19,406 [INFO] scraper: fetch_race 21/7: boats=6 odds=191/191
2026-08-14 11:29:19,410 [INFO] predictor: CALIBRATION_MODE=on
2026-08-14 11:29:19,410 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-14 11:29:19,414 [INFO] run_cycle: fetched 21/7 [final]: 156 combos
2026-08-14 11:29:19,631 [INFO] race_id: notif: nid=2026081421071132 sid=S00 phase=final rank=S
2026-08-14 11:29:20,002 [INFO] notifier: Discord notify OK (status=204)
2026-08-14 11:29:20,483 [INFO] notifier: Discord notify OK (status=204)
2026-08-14 11:29:20,488 [INFO] run_cycle: FINAL S00 芦屋7R S
2026-08-14 11:29:24,048 [INFO] scraper: odds3t: 120/120 parsed
2026-08-14 11:29:25,149 [INFO] scraper: odds3f: 20/20 parsed
2026-08-14 11:29:26,235 [INFO] scraper: odds2t: 30/30 parsed
2026-08-14 11:29:26,236 [INFO] scraper: odds2f: 15/15 parsed
2026-08-14 11:29:27,341 [INFO] scraper: odds_win: 4/6 parsed
2026-08-14 11:29:27,341 [INFO] scraper: fetch_race 08/3: boats=6 odds=189/191
2026-08-14 11:29:27,344 [INFO] predictor: CALIBRATION_MODE=on
2026-08-14 11:29:27,344 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-08-14 11:29:27,347 [INFO] run_cycle: fetched 08/3 [scan]: 154 combos
2026-08-14 11:29:29,665 [WARNING] scraper: beforeinfo parse failed: jcd=03 rno=2
2026-08-14 11:29:29,666 [WARNING] run_cycle: fetch None: 03/2
2026-08-14 11:29:29,666 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 96
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 96
  }
]
```

## Phase別通知記録 (24h)
{'final': 39, 'result': 19, 'scan': 38}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 163
  FINAL_MISSING: 142
  CIRCUIT_BREAKER_TRIP: 49
  ANOMALY_SCAN_FINAL_RATIO: 39
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 43 | 8 | 12,900 | 6,390 | -6,510 | 0.495 |
| S01_NAKAANA1 | 50 | 8 | 10,000 | 4,940 | -5,060 | 0.494 |
| S02_TETSUBAN | 23 | 12 | 4,600 | 3,620 | -980 | 0.787 |

## 直近アラート (24h・新しい順)
```
[11:17:35] CIRCUIT_BREAKER_TRIP: {"cost": 10000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 50, "payout": 4940, "roi_7d": 0.494, "sid": "S01_NAKAANA1"}
[11:17:34] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.234, "baseline_mean": 0.766, "baseline_stdev": 0.109, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 5, "z_score": 2.14}
[11:11:34] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.234, "baseline_mean": 0.766, "baseline_stdev": 0.109, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 4, "z_score": 2.14}
[11:02:26] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:02:26] CIRCUIT_BREAKER_TRIP: {"cost": 9800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 49, "payout": 4940, "roi_7d": 0.504, "sid": "S01_NAKAANA1"}
[11:02:26] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[11:02:26] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[10:57:26] CIRCUIT_BREAKER_TRIP: {"cost": 12600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 42, "payout": 6390, "roi_7d": 0.507, "sid": "S00"}
[10:47:26] CIRCUIT_BREAKER_TRIP: {"cost": 12900, "kind": "CIRCUIT_BREAKER_TRIP", "n": 43, "payout": 6390, "roi_7d": 0.495, "sid": "S00"}
[10:44:46] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.234, "baseline_mean": 0.766, "baseline_stdev": 0.109, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 3, "z_score": 2.14}
```

## 本日残レース: 162件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 192件 登録 / 30件 締切済
- 通知発射: scan=5 nid / final=6 nid / result=0 nid
- predictions: 2 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 217R | win | 1 | 0.2294 | 6.1 | 1.40 | 300 | scan=- drift=- | 11:29:19 |
| S01_NAKAANA1 | 107R | win | 1 | 0.3177 | 3.3 | 1.05 | 200 | scan=3.7 drift=-10.8% | 11:17:19 |
| S00 | 194R | win | 1 | 0.5334 | 5.5 | 2.93 | 300 | scan=4.2 drift=+31.0% | 19:00:22 |
| S00 | 019R | win | 1 | 0.1543 | 19.0 | 2.93 | 300 | scan=- drift=- | 18:49:30 |
| S02_TETSUBAN | 075R | win | 1 | 0.4111 | 2.2 | 0.90 | 200 | scan=- drift=- | 17:08:18 |
| S00 | 125R | win | 1 | 0.4111 | 4.1 | 1.69 | 300 | scan=- drift=- | 17:03:29 |
| S00 | 015R | win | 1 | 0.3177 | 4.3 | 1.37 | 300 | scan=11.6 drift=-62.9% | 16:58:31 |
| S02_TETSUBAN | 074R | win | 1 | 0.5476 | 2.1 | 1.15 | 200 | scan=- drift=- | 16:41:31 |
| S00 | 073R | win | 1 | 0.4111 | 4.8 | 1.97 | 300 | scan=- drift=- | 16:16:19 |
| S01_NAKAANA1 | 049R | win | 1 | 0.5123 | 3.1 | 1.59 | 200 | scan=3.0 drift=+3.3% | 16:02:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 69 | +5.7% | -62.9% | +287.7% | 21 | 8 | 45 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 492.4s |
| **Latency** (scan→final max) | 615.5s |
| **Traffic** (notifications 24h) | 96 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 407 | 0.4664 | 0.2654 | +0.2010 | 🟡+43% | 0.2361 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 171 | 0.4180 | 0.2164 | 0.2240 | 🔴-0.32 | 0.602 |
| S01_NAKAANA1 | win | 165 | 0.4902 | 0.2000 | 0.2469 | 🔴-0.54 | 0.605 |
| S02_TETSUBAN | win | 71 | 0.5276 | 0.5352 | 0.2401 | ✅+0.03 | 0.897 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1201 | 0.2000 | 🔴-0.0799 |
| 0.15-0.20 | 11 | 0.1834 | 0.0909 | 🔴+0.0924 |
| 0.20-0.30 | 9 | 0.2228 | 0.3333 | 🔴-0.1106 |
| 0.30-0.50 | 155 | 0.4194 | 0.2129 | 🔴+0.2065 |
| 0.50+ | 220 | 0.5428 | 0.3136 | 🔴+0.2292 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 108 | 0.771 |
| win | <5.0 | ✅learned | 182 | 0.724 |
| win | <10.0 | ✅learned | 92 | 0.449 |
| win | <20.0 | ✅learned | 30 | 0.227 |
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
_auto-generated by claude_snapshot.py at 2026-08-14T11:30:01.737482+09:00_