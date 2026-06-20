# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-20T15:40:02.193352+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×32 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×108 (24h)
- 🔴 PSI_DRIFT_DETECTED×32 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×14  [2026-06-20T15:25:54]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🔴 STRATEGY_CI_FAIL  ×36  [2026-06-20T15:03:35]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×40  [2026-06-20T13:29:00]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×17  [2026-06-20T13:02:35]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×3  [2026-06-20T12:19:49]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-06-20T11:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×59  [2026-06-20T10:00:27]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-20T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S00: n=144<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-20T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1835 actual=0.2000 gap=-0.0165`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-20T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-20T06:00:16]
- key: `ROI_STAT|S00: n=144 hit%=27.8% hit_CI[Bonf]=[18.4,39.5]% ROI=0.79 ROI_boot95=[0.55,1.04]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-20T06:00:16]
- key: `ROI_STAT|S01_NAKAANA1: n=136 hit%=29.4% hit_CI[Bonf]=[19.6,41.6]% ROI=0.77 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-20T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=136<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-20T06:00:16]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=35.9% hit_CI[Bonf]=[22.3,52.2]% ROI=0.58 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-20T06:00:16]
- key: `ORPHAN_SCAN|146 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-20T06:00:16]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=28.6% ROI=0.84 (コスト 10,100/回収 8,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-20T06:00:16]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=31 hit%=12.9% ROI=0.21 (コスト 6,900/回収 1,420)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-20T06:00:16]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=69 hit%=31.9% ROI=0.76 (コスト 16,200/回収 12,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-20T06:00:16]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=37 hit%=24.3% ROI=1.07 (コスト 8,700/回収 9,350)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-20T06:00:16]
- key: `DRIFT_BUCKET|drift ≥+30%: n=26 hit%=23.1% ROI=0.48 (コスト 7,200/回収 3,450)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.57MB / last modified 2026-06-20T15:39:23.721041+09:00

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
bos
2026-06-20 15:38:30,186 [INFO] scraper: odds3t: 120/120 parsed
2026-06-20 15:38:31,480 [INFO] scraper: odds3f: 20/20 parsed
2026-06-20 15:38:32,618 [INFO] scraper: odds2t: 30/30 parsed
2026-06-20 15:38:32,619 [INFO] scraper: odds2f: 15/15 parsed
2026-06-20 15:38:33,718 [INFO] scraper: odds_win: 3/6 parsed
2026-06-20 15:38:33,718 [INFO] scraper: fetch_race 24/2: boats=6 odds=188/191
2026-06-20 15:38:33,728 [INFO] predictor: CALIBRATION_MODE=on
2026-06-20 15:38:33,728 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-06-20 15:38:33,736 [INFO] run_cycle: fetched 24/2 [scan]: 153 combos
2026-06-20 15:38:33,852 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-20 15:39:06,132 [INFO] run_cycle: === run_cycle 15:39:06 ===
2026-06-20 15:39:06,132 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-20 15:39:06,133 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-20 15:39:06,214 [INFO] predictor: Models loaded OK
2026-06-20 15:39:18,702 [INFO] scraper: odds3t: 120/120 parsed
2026-06-20 15:39:19,933 [INFO] scraper: odds3f: 20/20 parsed
2026-06-20 15:39:21,053 [INFO] scraper: odds2t: 30/30 parsed
2026-06-20 15:39:21,054 [INFO] scraper: odds2f: 13/15 parsed
2026-06-20 15:39:22,279 [INFO] scraper: odds_win: 5/6 parsed
2026-06-20 15:39:22,279 [INFO] scraper: fetch_race 15/2: boats=6 odds=188/191
2026-06-20 15:39:22,291 [INFO] predictor: CALIBRATION_MODE=on
2026-06-20 15:39:22,291 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-06-20 15:39:22,300 [INFO] run_cycle: fetched 15/2 [final]: 155 combos
2026-06-20 15:39:22,501 [INFO] race_id: notif: nid=2026062015021542 sid=S00 phase=final rank=
2026-06-20 15:39:22,876 [INFO] notifier: Discord notify OK (status=204)
2026-06-20 15:39:23,291 [INFO] notifier: Discord notify OK (status=204)
2026-06-20 15:39:23,360 [INFO] run_cycle: RETREAT S00 丸亀2R
2026-06-20 15:39:23,669 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 114
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 114
  }
]
```

## Phase別通知記録 (24h)
{'final': 47, 'result': 20, 'scan': 47}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 136
  FINAL_MISSING: 108
  PSI_DRIFT_DETECTED: 32
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 9
  ANOMALY_SCAN_FINAL_RATIO: 2
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 32 | 10 | 9,600 | 7,890 | -1,710 | 0.822 |
| S01_NAKAANA1 | 34 | 9 | 6,800 | 5,220 | -1,580 | 0.768 |
| S02_TETSUBAN | 13 | 6 | 2,600 | 2,240 | -360 | 0.862 |

## 直近アラート (24h・新しい順)
```
[15:30:47] FINAL_MISSING: {"deadline": "2026-06-20T15:00:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062004071500", "sid": "S00"}
[15:25:54] FINAL_MISSING: {"deadline": "2026-06-20T13:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062004051355", "sid": "S00"}
[15:25:54] FINAL_MISSING: {"deadline": "2026-06-20T12:54:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062004031254", "sid": "S00"}
[15:25:54] FINAL_MISSING: {"deadline": "2026-06-20T11:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062004011155", "sid": "S00"}
[15:18:31] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 8.6, "baseline_n_days": 7, "baseline_stdev": 3.5, "hour": 15, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 18, "z_score": 2.69}
[15:06:48] FINAL_MISSING: {"deadline": "2026-06-20T10:36:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062013011036", "sid": "S00"}
[15:05:52] FINAL_MISSING: {"deadline": "2026-06-20T12:35:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062005031235", "sid": "S00"}
[15:03:35] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:00:44] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 8.6, "baseline_n_days": 7, "baseline_stdev": 3.5, "hour": 15, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 17, "z_score": 2.4}
[14:58:29] FINAL_MISSING: {"deadline": "2026-06-20T14:28:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062004061428", "sid": "S00"}
```

## 本日残レース: 63件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 105件 締切済
- 通知発射: scan=31 nid / final=34 nid / result=16 nid
- predictions: 18 / うち結果DB記録済: 17
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 7件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 0210R | win | 1 | 0.5123 | 4.4 | 2.25 | 200 | scan=4.5 drift=-2.2% | 15:18:22 |
| S00 | 057R | win | 1 | 0.4111 | 6.7 | 2.75 | 300 | scan=- drift=- | 14:32:21 |
| S01_NAKAANA1 | 066R | win | 1 | 0.5334 | 4.0 | 2.13 | 200 | scan=- drift=- | 13:59:34 |
| S00 | 066R | win | 1 | 0.5334 | 4.0 | 2.13 | 300 | scan=6.2 drift=-35.5% | 13:59:32 |
| S01_NAKAANA1 | 045R | win | 1 | 0.5735 | 3.1 | 1.78 | 200 | scan=4.3 drift=-27.9% | 13:52:20 |
| S01_NAKAANA1 | 097R | win | 1 | 0.5334 | 3.7 | 1.97 | 200 | scan=3.7 drift=+0.0% | 13:38:21 |
| S00 | 117R | win | 1 | 0.4989 | 12.7 | 6.34 | 300 | scan=- drift=- | 13:27:22 |
| S00 | 065R | win | 1 | 0.5174 | 4.3 | 2.22 | 300 | scan=- drift=- | 13:25:35 |
| S00 | 176R | win | 1 | 0.0754 | 6.0 | 0.45 | 300 | scan=4.5 drift=+33.3% | 13:20:27 |
| S02_TETSUBAN | 136R | win | 1 | 0.5123 | 2.1 | 1.08 | 200 | scan=- drift=- | 13:05:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 48 | -6.7% | -61.4% | +43.3% | 19 | 10 | 30 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 514.9s |
| **Latency** (scan→final max) | 647.6s |
| **Traffic** (notifications 24h) | 114 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,100円 used |
| **Saturation** (S01_NAKAANA1) | 1,600円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 367 | 0.4711 | 0.2970 | +0.1741 | 🟡+37% | 0.2398 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 146 | 0.4196 | 0.2671 | 0.2200 | 🔴-0.12 | 0.762 |
| S01_NAKAANA1 | win | 141 | 0.4874 | 0.2837 | 0.2450 | 🔴-0.21 | 0.741 |
| S02_TETSUBAN | win | 80 | 0.5364 | 0.3750 | 0.2670 | 🔴-0.14 | 0.634 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0816 | 0.0000 | 🔴+0.0816 |
| 0.15-0.20 | 6 | 0.1816 | 0.3333 | 🔴-0.1518 |
| 0.20-0.30 | 10 | 0.2246 | 0.1000 | 🔴+0.1246 |
| 0.30-0.50 | 130 | 0.4211 | 0.2615 | 🔴+0.1596 |
| 0.50+ | 210 | 0.5426 | 0.3381 | 🔴+0.2045 |

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
_auto-generated by claude_snapshot.py at 2026-06-20T15:40:02.193352+09:00_