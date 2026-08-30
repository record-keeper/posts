# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-30T14:00:02.034250+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×41 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×41 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 FINAL_MISSING×5 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×29  [2026-08-30T13:13:58]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×114  [2026-08-30T13:03:31]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×114  [2026-08-30T13:03:31]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×57  [2026-08-30T13:03:31]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×47  [2026-08-30T13:02:27]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-30T13:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-30T13:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×2  [2026-08-30T12:59:38]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ORPHAN_SCAN  ×1  [2026-08-30T06:00:10]
- key: `ORPHAN_SCAN|195 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-30T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=83<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-30T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=171<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-30T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=30.2% ROI=0.94 (コスト 10,000/回収 9,380)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-30T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=12 pred=0.1819 actual=0.1667 gap=+0.0152`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-30T06:00:10]
- key: `ROI_STAT|S00: n=171 hit%=26.9% hit_CI[Bonf]=[18.4,37.6]% ROI=0.87 ROI_boot95=[0.62,1.15]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-30T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=188 hit%=25.5% hit_CI[Bonf]=[17.5,35.6]% ROI=0.81 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-30T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=188<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-30T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=83 hit%=39.8% hit_CI[Bonf]=[25.9,55.5]% ROI=0.66 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-30T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=38 hit%=15.8% ROI=0.42 (コスト 11,000/回収 4,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-30T06:00:10]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=95 hit%=28.4% ROI=0.93 (コスト 21,700/回収 20,110)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-30T06:00:10]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=52 hit%=26.9% ROI=0.53 (コスト 11,800/回収 6,220)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.83MB / last modified 2026-08-30T14:00:03.601352+09:00

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
 run_cycle 13:58:03 ===
2026-08-30 13:58:03,937 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-30 13:58:03,937 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-30 13:58:03,966 [INFO] predictor: Models loaded OK
2026-08-30 13:58:04,068 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-30 13:59:03,903 [INFO] run_cycle: === run_cycle 13:59:03 ===
2026-08-30 13:59:03,903 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-30 13:59:03,903 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-30 13:59:03,950 [INFO] predictor: Models loaded OK
2026-08-30 13:59:15,361 [INFO] scraper: odds3t: 120/120 parsed
2026-08-30 13:59:16,475 [INFO] scraper: odds3f: 20/20 parsed
2026-08-30 13:59:17,575 [INFO] scraper: odds2t: 30/30 parsed
2026-08-30 13:59:17,576 [INFO] scraper: odds2f: 15/15 parsed
2026-08-30 13:59:18,688 [INFO] scraper: odds_win: 6/6 parsed
2026-08-30 13:59:18,688 [INFO] scraper: fetch_race 05/6: boats=6 odds=191/191
2026-08-30 13:59:18,692 [INFO] predictor: CALIBRATION_MODE=on
2026-08-30 13:59:18,692 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-30 13:59:18,697 [INFO] run_cycle: fetched 05/6 [final]: 156 combos
2026-08-30 13:59:22,305 [INFO] scraper: odds3t: 120/120 parsed
2026-08-30 13:59:23,405 [INFO] scraper: odds3f: 20/20 parsed
2026-08-30 13:59:24,517 [INFO] scraper: odds2t: 30/30 parsed
2026-08-30 13:59:24,518 [INFO] scraper: odds2f: 15/15 parsed
2026-08-30 13:59:25,594 [INFO] scraper: odds_win: 5/6 parsed
2026-08-30 13:59:25,594 [INFO] scraper: fetch_race 21/12: boats=6 odds=190/191
2026-08-30 13:59:25,597 [INFO] predictor: CALIBRATION_MODE=on
2026-08-30 13:59:25,597 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-30 13:59:25,602 [INFO] run_cycle: fetched 21/12 [scan]: 155 combos
2026-08-30 13:59:25,727 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 18, 'result': 6, 'scan': 17}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 152
  CIRCUIT_BREAKER_TRIP: 41
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_SCAN_FINAL_RATIO: 28
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 6
  FINAL_MISSING: 5
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 39 | 9 | 11,700 | 9,780 | -1,920 | 0.836 |
| S01_NAKAANA1 | 42 | 10 | 8,400 | 4,940 | -3,460 | 0.588 |
| S02_TETSUBAN | 21 | 6 | 4,200 | 2,460 | -1,740 | 0.586 |

## 直近アラート (24h・新しい順)
```
[13:56:20] FINAL_MISSING: {"deadline": "2026-08-30T12:25:00+09:00", "kind": "FINAL_MISSING", "nid": "2026083021091225", "sid": "S00"}
[13:48:25] FINAL_MISSING: {"deadline": "2026-08-30T12:17:00+09:00", "kind": "FINAL_MISSING", "nid": "2026083004021217", "sid": "S00"}
[13:41:42] CIRCUIT_BREAKER_TRIP: {"cost": 4200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 21, "payout": 2460, "roi_7d": 0.586, "sid": "S02_TETSUBAN"}
[13:41:42] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 9.1, "baseline_n_days": 7, "baseline_stdev": 3.2, "hour": 13, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 2, "z_score": -2.21}
[13:39:30] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.201, "baseline_mean": 0.838, "baseline_stdev": 0.081, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.636, "today_scan_count": 11, "z_score": -2.47}
[13:30:46] FINAL_MISSING: {"deadline": "2026-08-30T13:00:00+09:00", "kind": "FINAL_MISSING", "nid": "2026083005041300", "sid": "S00"}
[13:25:29] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.238, "baseline_mean": 0.838, "baseline_stdev": 0.081, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.6, "today_scan_count": 10, "z_score": -2.92}
[13:24:30] CIRCUIT_BREAKER_TRIP: {"cost": 8400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 42, "payout": 4940, "roi_7d": 0.588, "sid": "S01_NAKAANA1"}
[13:13:58] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.171, "baseline_mean": 0.838, "baseline_stdev": 0.081, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 9, "z_score": -2.1}
[13:06:38] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.282, "baseline_mean": 0.838, "baseline_stdev": 0.081, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.556, "today_scan_count": 9, "z_score": -3.47}
```

## 本日残レース: 83件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 85件 締切済
- 通知発射: scan=11 nid / final=10 nid / result=1 nid
- predictions: 3 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 166R | win | 1 | 0.3177 | 11.2 | 3.56 | 300 | scan=5.2 drift=+115.4% | 13:49:18 |
| S02_TETSUBAN | 117R | win | 1 | 0.5123 | 2.3 | 1.18 | 200 | scan=- drift=- | 13:41:30 |
| S01_NAKAANA1 | 164R | win | 1 | 0.5476 | 3.0 | 1.64 | 200 | scan=- drift=- | 12:47:30 |
| S00 | 192R | win | 1 | 0.1084 | 5.5 | 0.60 | 300 | scan=5.6 drift=-1.8% | 15:46:30 |
| S02_TETSUBAN | 059R | win | 1 | 0.4989 | 2.6 | 1.30 | 200 | scan=- drift=- | 15:35:30 |
| S01_NAKAANA1 | 057R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=- drift=- | 14:29:25 |
| S01_NAKAANA1 | 045R | win | 1 | 0.5174 | 3.0 | 1.55 | 200 | scan=3.0 drift=+0.0% | 13:44:44 |
| S01_NAKAANA1 | 137R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=3.6 drift=+22.2% | 13:36:18 |
| S02_TETSUBAN | 117R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=2.0 drift=+5.0% | 13:23:31 |
| S01_NAKAANA1 | 115R | win | 1 | 0.4989 | 3.3 | 1.65 | 200 | scan=- drift=- | 12:27:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 60 | +5.0% | -79.6% | +320.7% | 21 | 9 | 42 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 561.5s |
| **Latency** (scan→final max) | 660.8s |
| **Traffic** (notifications 24h) | 41 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 433 | 0.4726 | 0.2887 | +0.1839 | 🟡+39% | 0.2402 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 166 | 0.4132 | 0.2771 | 0.2166 | 🔴-0.08 | 0.893 |
| S01_NAKAANA1 | win | 185 | 0.4920 | 0.2486 | 0.2514 | 🔴-0.35 | 0.753 |
| S02_TETSUBAN | win | 82 | 0.5489 | 0.4024 | 0.2626 | 🔴-0.09 | 0.672 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1221 | 0.1000 | ✅+0.0221 |
| 0.15-0.20 | 12 | 0.1819 | 0.1667 | ✅+0.0152 |
| 0.20-0.30 | 9 | 0.2251 | 0.2222 | ✅+0.0029 |
| 0.30-0.50 | 145 | 0.4119 | 0.2483 | 🔴+0.1637 |
| 0.50+ | 255 | 0.5463 | 0.3294 | 🔴+0.2168 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 124 | 0.775 |
| win | <5.0 | ✅learned | 225 | 0.745 |
| win | <10.0 | ✅learned | 109 | 0.458 |
| win | <20.0 | ✅learned | 30 | 0.227 |
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
_auto-generated by claude_snapshot.py at 2026-08-30T14:00:02.034250+09:00_