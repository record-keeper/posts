# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-20T12:30:01.893854+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×41 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×92 (24h)
- 🔴 PSI_DRIFT_DETECTED×41 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-20T12:30:06]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×4  [2026-09-20T12:07:26]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×26  [2026-09-20T12:03:28]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×26  [2026-09-20T12:03:28]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×26  [2026-09-20T12:03:28]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×26  [2026-09-20T12:03:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×33  [2026-09-20T10:45:55]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_DROP  ×49  [2026-09-20T10:00:08]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-20T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=76<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-20T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=173<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-20T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-20T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1314 actual=0.0000 gap=+0.1314`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-20T06:00:12]
- key: `ROI_STAT|S00: n=173 hit%=24.3% hit_CI[Bonf]=[16.2,34.7]% ROI=0.75 ROI_boot95=[0.52,1.03]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-20T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=167 hit%=21.0% hit_CI[Bonf]=[13.4,31.3]% ROI=0.62 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-20T06:00:12]
- key: `ROI_STAT|S02_TETSUBAN: n=76 hit%=40.8% hit_CI[Bonf]=[26.2,57.2]% ROI=0.75 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-09-20T06:00:12]
- key: `ORPHAN_SCAN|181 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-20T06:00:12]
- key: `DRIFT_BUCKET|drift ≤-30%: n=32 hit%=28.1% ROI=0.84 (コスト 9,200/回収 7,760)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-20T06:00:12]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=38 hit%=18.4% ROI=0.55 (コスト 8,800/回収 4,800)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-20T06:00:12]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=83 hit%=24.1% ROI=0.72 (コスト 19,300/回収 13,880)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-20T06:00:12]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=49 hit%=22.4% ROI=0.47 (コスト 10,800/回収 5,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.72MB / last modified 2026-09-20T12:30:06.890692+09:00

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
rsed
2026-09-20 12:28:29,016 [INFO] scraper: fetch_race 06/3: boats=6 odds=191/191
2026-09-20 12:28:29,018 [INFO] predictor: CALIBRATION_MODE=on
2026-09-20 12:28:29,018 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-20 12:28:29,022 [INFO] run_cycle: fetched 06/3 [scan]: 156 combos
2026-09-20 12:28:29,466 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-20 12:29:04,562 [INFO] run_cycle: === run_cycle 12:29:04 ===
2026-09-20 12:29:04,563 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-20 12:29:04,563 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-20 12:29:04,643 [INFO] predictor: Models loaded OK
2026-09-20 12:29:16,197 [INFO] scraper: odds3t: 120/120 parsed
2026-09-20 12:29:17,304 [INFO] scraper: odds3f: 20/20 parsed
2026-09-20 12:29:18,384 [INFO] scraper: odds2t: 30/30 parsed
2026-09-20 12:29:18,386 [INFO] scraper: odds2f: 15/15 parsed
2026-09-20 12:29:19,498 [INFO] scraper: odds_win: 6/6 parsed
2026-09-20 12:29:19,498 [INFO] scraper: fetch_race 14/9: boats=6 odds=191/191
2026-09-20 12:29:19,501 [INFO] predictor: CALIBRATION_MODE=on
2026-09-20 12:29:19,501 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-20 12:29:19,505 [INFO] run_cycle: fetched 14/9 [final]: 156 combos
2026-09-20 12:29:23,047 [INFO] scraper: odds3t: 120/120 parsed
2026-09-20 12:29:24,277 [INFO] scraper: odds3f: 20/20 parsed
2026-09-20 12:29:25,363 [INFO] scraper: odds2t: 30/30 parsed
2026-09-20 12:29:25,364 [INFO] scraper: odds2f: 15/15 parsed
2026-09-20 12:29:26,470 [INFO] scraper: odds_win: 6/6 parsed
2026-09-20 12:29:26,470 [INFO] scraper: fetch_race 03/4: boats=6 odds=191/191
2026-09-20 12:29:26,473 [INFO] predictor: CALIBRATION_MODE=on
2026-09-20 12:29:26,473 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-20 12:29:26,477 [INFO] run_cycle: fetched 03/4 [scan]: 156 combos
2026-09-20 12:29:26,790 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 67
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 67
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 12, 'scan': 30}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 92
  ANOMALY_SCRAPER_FAILURE_BURST: 64
  PSI_DRIFT_DETECTED: 41
  CIRCUIT_BREAKER_TRIP: 22
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 8
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 44 | 11 | 13,200 | 9,180 | -4,020 | 0.695 |
| S01_NAKAANA1 | 36 | 12 | 7,200 | 8,480 | +1,280 | 1.178 |
| S02_TETSUBAN | 18 | 9 | 3,600 | 3,680 | +80 | 1.022 |

## 直近アラート (24h・新しい順)
```
[12:17:32] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 316, "n_recent": 98, "psi": 0.352}
[12:17:32] FINAL_MISSING: {"deadline": "2026-09-20T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092002011047", "sid": "S01_NAKAANA1"}
[12:11:48] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 316, "n_recent": 97, "psi": 0.351}
[12:11:48] FINAL_MISSING: {"deadline": "2026-09-20T11:41:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092003021141", "sid": "S00"}
[12:07:25] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.223, "baseline_mean": 0.795, "baseline_stdev": 0.082, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.571, "today_scan_count": 7, "z_score": -2.71}
[12:03:27] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:03:27] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 317, "n_recent": 96, "psi": 0.349}
[12:03:27] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[11:59:45] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 318, "n_recent": 96, "psi": 0.348}
[11:54:28] CIRCUIT_BREAKER_TRIP: {"cost": 13200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 44, "payout": 9180, "roi_7d": 0.695, "sid": "S00"}
```

## 本日残レース: 116件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 52件 締切済
- 通知発射: scan=8 nid / final=7 nid / result=3 nid
- predictions: 5 / うち結果DB記録済: 3
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 135R | win | 1 | 0.5334 | 2.0 | 1.07 | 200 | scan=- drift=- | 12:17:21 |
| S01_NAKAANA1 | 024R | win | 1 | 0.5123 | 3.3 | 1.69 | 200 | scan=- drift=- | 12:11:45 |
| S01_NAKAANA1 | 032R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=4.5 drift=-20.0% | 11:38:20 |
| S01_NAKAANA1 | 173R | win | 1 | 0.3177 | 4.7 | 1.49 | 200 | scan=3.4 drift=+38.2% | 11:34:19 |
| S01_NAKAANA1 | 146R | win | 1 | 0.5123 | 3.5 | 1.79 | 200 | scan=3.1 drift=+12.9% | 10:49:18 |
| S00 | 128R | win | 1 | 0.5334 | 5.1 | 2.72 | 300 | scan=5.2 drift=-1.9% | 18:23:18 |
| S01_NAKAANA1 | 0411R | win | 1 | 0.4111 | 3.8 | 1.56 | 200 | scan=4.1 drift=-7.3% | 16:03:31 |
| S01_NAKAANA1 | 151R | win | 1 | 0.5735 | 3.3 | 1.89 | 200 | scan=- drift=- | 15:19:36 |
| S00 | 0210R | win | 1 | 0.4989 | 4.1 | 2.05 | 300 | scan=- drift=- | 15:19:20 |
| S01_NAKAANA1 | 028R | win | 1 | 0.3177 | 3.8 | 1.21 | 200 | scan=3.2 drift=+18.7% | 14:13:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 59 | +3.3% | -81.7% | +119.5% | 15 | 5 | 37 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 437.7s |
| **Latency** (scan→final max) | 613.4s |
| **Traffic** (notifications 24h) | 67 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 412 | 0.4776 | 0.2646 | +0.2131 | 🟡+45% | 0.2410 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 169 | 0.4426 | 0.2426 | 0.2270 | 🔴-0.24 | 0.754 |
| S01_NAKAANA1 | win | 169 | 0.4851 | 0.2189 | 0.2460 | 🔴-0.44 | 0.645 |
| S02_TETSUBAN | win | 74 | 0.5405 | 0.4189 | 0.2616 | 🔴-0.07 | 0.77 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 5 | 0.1279 | 0.0000 | 🔴+0.1279 |
| 0.30-0.50 | 150 | 0.4092 | 0.2200 | 🔴+0.1892 |
| 0.50+ | 244 | 0.5442 | 0.3033 | 🔴+0.2409 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 145 | 0.775 |
| win | <5.0 | ✅learned | 258 | 0.76 |
| win | <10.0 | ✅learned | 126 | 0.46 |
| win | <20.0 | ✅learned | 33 | 0.234 |
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
_auto-generated by claude_snapshot.py at 2026-09-20T12:30:01.893854+09:00_