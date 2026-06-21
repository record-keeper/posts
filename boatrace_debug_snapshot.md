# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-21T11:40:01.609236+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×80 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×10 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×3 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×37  [2026-06-21T11:03:29]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×9  [2026-06-21T11:00:33]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-21T11:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×58  [2026-06-21T10:42:39]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 CIRCUIT_BREAKER_TRIP  ×59  [2026-06-21T10:41:27]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-21T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=141<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-21T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=146<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-21T06:00:10]
- key: `DRIFT_BUCKET|drift ≥+30%: n=26 hit%=23.1% ROI=0.48 (コスト 7,200/回収 3,450)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-21T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2246 actual=0.1000 gap=+0.1246`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-21T06:00:10]
- key: `ROI_STAT|S00: n=146 hit%=26.7% hit_CI[Bonf]=[17.6,38.3]% ROI=0.76 ROI_boot95=[0.53,1.03]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-21T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=141 hit%=28.4% hit_CI[Bonf]=[18.9,40.3]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-21T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=81 hit%=37.0% hit_CI[Bonf]=[23.4,53.0]% ROI=0.63 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-21T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-21T06:00:10]
- key: `ORPHAN_SCAN|154 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-21T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=36 hit%=22.2% ROI=0.66 (コスト 10,300/回収 6,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-21T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=33 hit%=15.2% ROI=0.24 (コスト 7,300/回収 1,740)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-21T06:00:10]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=72 hit%=31.9% ROI=0.76 (コスト 16,900/回収 12,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-21T06:00:10]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=36 hit%=25.0% ROI=1.10 (コスト 8,500/回収 9,350)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-21T06:00:10]
- key: `CALIBRATION_LIVE|bt=win: n=368 pred=0.4718 actual=0.2962 error=+0.1756 (+37%) brier=0.2404 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-21T06:00:10]
- key: `CALIBRATION_LIVE|S00(win): n=146 pred=0.4202 hit=0.2671 cal_err=+0.1531 brier=0.2205 BSS=-0.13 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.62MB / last modified 2026-06-21T11:39:21.869498+09:00

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
22,436 [INFO] run_cycle: fetched 11/3 [final]: 156 combos
2026-06-21 11:37:25,188 [WARNING] scraper: beforeinfo parse failed: jcd=10 rno=8
2026-06-21 11:37:25,188 [WARNING] run_cycle: fetch None: 10/8
2026-06-21 11:37:25,188 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-21 11:38:05,877 [INFO] run_cycle: === run_cycle 11:38:05 ===
2026-06-21 11:38:05,877 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-21 11:38:05,877 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-21 11:38:05,925 [INFO] predictor: Models loaded OK
2026-06-21 11:38:16,394 [WARNING] scraper: beforeinfo parse failed: jcd=10 rno=8
2026-06-21 11:38:16,394 [WARNING] run_cycle: fetch None: 10/8
2026-06-21 11:38:16,395 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-21 11:39:03,901 [INFO] run_cycle: === run_cycle 11:39:03 ===
2026-06-21 11:39:03,901 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-21 11:39:03,901 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-21 11:39:03,946 [INFO] predictor: Models loaded OK
2026-06-21 11:39:14,609 [WARNING] scraper: beforeinfo parse failed: jcd=10 rno=8
2026-06-21 11:39:14,609 [WARNING] run_cycle: fetch None: 10/8
2026-06-21 11:39:18,217 [INFO] scraper: odds3t: 120/120 parsed
2026-06-21 11:39:19,319 [INFO] scraper: odds3f: 19/20 parsed
2026-06-21 11:39:20,485 [INFO] scraper: odds2t: 26/30 parsed
2026-06-21 11:39:20,486 [INFO] scraper: odds2f: 12/15 parsed
2026-06-21 11:39:21,659 [INFO] scraper: odds_win: 6/6 parsed
2026-06-21 11:39:21,659 [INFO] scraper: fetch_race 13/4: boats=6 odds=183/191
2026-06-21 11:39:21,671 [INFO] predictor: CALIBRATION_MODE=on
2026-06-21 11:39:21,671 [INFO] predictor: combos: {'win': 6, '2t': 26, '3t': 120}
2026-06-21 11:39:21,678 [INFO] run_cycle: fetched 13/4 [scan]: 152 combos
2026-06-21 11:39:21,771 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 97
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 97
  }
]
```

## Phase別通知記録 (24h)
{'final': 41, 'result': 20, 'scan': 36}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 98
  FINAL_MISSING: 80
  ANOMALY_BET_VOLUME_SPIKE: 19
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 10
  CIRCUIT_BREAKER_TRIP: 3
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 2
  ANOMALY_SCAN_FINAL_RATIO: 1
  CIRCUIT_BREAKER_NO_ACTION: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 32 | 9 | 9,600 | 6,750 | -2,850 | 0.703 |
| S01_NAKAANA1 | 35 | 8 | 7,000 | 4,460 | -2,540 | 0.637 |
| S02_TETSUBAN | 13 | 5 | 2,600 | 1,920 | -680 | 0.738 |

## 直近アラート (24h・新しい順)
```
[11:13:35] CIRCUIT_BREAKER_TRIP: {"cost": 7000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 4460, "roi_7d": 0.637, "sid": "S01_NAKAANA1"}
[11:09:31] CIRCUIT_BREAKER_TRIP: {"cost": 6800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 4460, "roi_7d": 0.656, "sid": "S01_NAKAANA1"}
[11:03:29] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:00:33] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 3.1, "baseline_n_days": 7, "baseline_stdev": 1.3, "hour": 11, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 0, "z_score": -2.34}
[10:42:38] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[10:41:27] CIRCUIT_BREAKER_TRIP: {"cost": 6600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 33, "payout": 4460, "roi_7d": 0.676, "sid": "S01_NAKAANA1"}
[10:03:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:00:26] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 1.6, "baseline_n_days": 5, "baseline_stdev": 0.5, "hour": 10, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 0, "z_score": -2.92}
[09:02:33] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:01:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 158件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 192件 登録 / 34件 締切済
- 通知発射: scan=2 nid / final=3 nid / result=0 nid
- predictions: 2 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 162R | win | 1 | 0.5735 | 3.5 | 2.01 | 200 | scan=- drift=- | 11:13:20 |
| S01_NAKAANA1 | 107R | win | 1 | 0.5174 | 4.6 | 2.38 | 200 | scan=- drift=- | 11:09:21 |
| S02_TETSUBAN | 2012R | win | 1 | 0.5312 | 2.7 | 1.43 | 200 | scan=- drift=- | 22:51:21 |
| S00 | 154R | win | 1 | 0.4989 | 5.8 | 2.89 | 300 | scan=11.4 drift=-49.1% | 16:36:20 |
| S01_NAKAANA1 | 0210R | win | 1 | 0.5123 | 4.4 | 2.25 | 200 | scan=4.5 drift=-2.2% | 15:18:22 |
| S00 | 057R | win | 1 | 0.4111 | 6.7 | 2.75 | 300 | scan=- drift=- | 14:32:21 |
| S01_NAKAANA1 | 066R | win | 1 | 0.5334 | 4.0 | 2.13 | 200 | scan=- drift=- | 13:59:34 |
| S00 | 066R | win | 1 | 0.5334 | 4.0 | 2.13 | 300 | scan=6.2 drift=-35.5% | 13:59:32 |
| S01_NAKAANA1 | 045R | win | 1 | 0.5735 | 3.1 | 1.78 | 200 | scan=4.3 drift=-27.9% | 13:52:20 |
| S01_NAKAANA1 | 097R | win | 1 | 0.5334 | 3.7 | 1.97 | 200 | scan=3.7 drift=+0.0% | 13:38:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 46 | -8.4% | -61.4% | +43.3% | 20 | 11 | 30 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 529.9s |
| **Latency** (scan→final max) | 617.6s |
| **Traffic** (notifications 24h) | 97 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 364 | 0.4726 | 0.2967 | +0.1759 | 🟡+37% | 0.2412 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 144 | 0.4223 | 0.2708 | 0.2225 | 🔴-0.13 | 0.772 |
| S01_NAKAANA1 | win | 141 | 0.4881 | 0.2837 | 0.2457 | 🔴-0.21 | 0.741 |
| S02_TETSUBAN | win | 79 | 0.5366 | 0.3671 | 0.2674 | 🔴-0.15 | 0.619 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0816 | 0.0000 | 🔴+0.0816 |
| 0.15-0.20 | 6 | 0.1816 | 0.3333 | 🔴-0.1518 |
| 0.20-0.30 | 9 | 0.2241 | 0.1111 | 🔴+0.1130 |
| 0.30-0.50 | 128 | 0.4227 | 0.2656 | 🔴+0.1571 |
| 0.50+ | 210 | 0.5425 | 0.3333 | 🔴+0.2092 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 46 | 0.733 |
| win | <5.0 | ✅learned | 85 | 0.743 |
| win | <10.0 | ✅learned | 55 | 0.495 |
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
_auto-generated by claude_snapshot.py at 2026-06-21T11:40:01.609236+09:00_