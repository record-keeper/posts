# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-27T15:00:01.737794+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×31 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×111 (24h)
- 🔴 PSI_DRIFT_DETECTED×31 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-27T15:00:06]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×3  [2026-11-27T14:51:15]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-27T14:30:08]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 STRATEGY_CI_FAIL  ×16  [2026-11-27T14:20:27]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×19  [2026-11-27T14:05:15]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-27T14:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 10 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-27T13:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 PSI_DRIFT_DETECTED  ×7  [2026-11-27T13:19:37]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-27T13:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-27T12:00:05]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 9 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×45  [2026-11-27T09:01:30]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ ROI_STAT  ×1  [2026-11-27T06:00:12]
- key: `ROI_STAT|S00: n=55 hit%=16.4% hit_CI[Bonf]=[6.7,34.9]% ROI=0.44 ROI_boot95=[0.17,0.78]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-27T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=55<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-27T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=80 hit%=33.8% hit_CI[Bonf]=[20.7,49.9]% ROI=0.90 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-27T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-27T06:00:12]
- key: `ROI_STAT|S02_TETSUBAN: n=38 hit%=42.1% hit_CI[Bonf]=[22.5,64.5]% ROI=0.93 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-27T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=38<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-11-27T06:00:12]
- key: `ORPHAN_SCAN|282 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-27T06:00:12]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=34 hit%=50.0% ROI=1.33 (コスト 7,700/回収 10,210)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-27T06:00:12]
- key: `CALIBRATION_LIVE|bt=win: n=173 pred=0.4718 actual=0.3006 error=+0.1712 (+36%) brier=0.2335 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 18.79MB / last modified 2026-11-27T14:59:06.644598+09:00

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
N_MODE=on
2026-11-27 14:56:36,590 [INFO] predictor: combos: {'win': 2, '2t': 29, '3t': 120}
2026-11-27 14:56:36,594 [INFO] run_cycle: fetched 13/10 [scan]: 151 combos
2026-11-27 14:56:36,738 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-27 14:57:04,914 [INFO] run_cycle: === run_cycle 14:57:04 ===
2026-11-27 14:57:04,915 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-27 14:57:04,915 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-27 14:57:04,982 [INFO] predictor: Models loaded OK
2026-11-27 14:57:32,421 [INFO] scraper: odds3t: 120/120 parsed
2026-11-27 14:57:41,559 [INFO] scraper: odds3f: 20/20 parsed
2026-11-27 14:57:51,644 [INFO] scraper: odds2t: 30/30 parsed
2026-11-27 14:57:51,645 [INFO] scraper: odds2f: 15/15 parsed
2026-11-27 14:58:00,716 [INFO] scraper: odds_win: 4/6 parsed
2026-11-27 14:58:00,716 [INFO] scraper: fetch_race 03/10: boats=6 odds=189/191
2026-11-27 14:58:00,731 [INFO] predictor: CALIBRATION_MODE=on
2026-11-27 14:58:00,731 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-11-27 14:58:00,734 [INFO] run_cycle: fetched 03/10 [final]: 154 combos
2026-11-27 14:58:03,894 [INFO] race_id: notif: nid=2026112703101459 sid=S02_TETSUBAN phase=final rank=
2026-11-27 14:58:04,436 [INFO] notifier: Discord notify OK (status=204)
2026-11-27 14:58:06,402 [INFO] notifier: Discord notify OK (status=204)
2026-11-27 14:58:06,449 [INFO] run_cycle: RETREAT S02_TETSUBAN 江戸川10R
2026-11-27 14:58:06,932 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-27 14:59:05,293 [INFO] run_cycle: === run_cycle 14:59:05 ===
2026-11-27 14:59:05,294 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-27 14:59:05,294 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-27 14:59:05,328 [INFO] predictor: Models loaded OK
2026-11-27 14:59:05,483 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 38
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 38
  }
]
```

## Phase別通知記録 (24h)
{'final': 14, 'result': 8, 'scan': 16}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 217
  FINAL_MISSING: 111
  PSI_DRIFT_DETECTED: 31
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 15 | 3 | 4,500 | 2,190 | -2,310 | 0.487 |
| S01_NAKAANA1 | 23 | 11 | 4,600 | 5,600 | +1,000 | 1.217 |
| S02_TETSUBAN | 11 | 5 | 2,200 | 3,260 | +1,060 | 1.482 |

## 直近アラート (24h・新しい順)
```
[14:59:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 476}
[14:58:07] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 478}
[14:56:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 469}
[14:53:13] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 478}
[14:51:12] FINAL_MISSING: {"deadline": "2026-11-27T12:17:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112703041217", "sid": "S00"}
[14:51:12] FINAL_MISSING: {"deadline": "2026-11-27T11:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112702021112", "sid": "S01_NAKAANA1"}
[14:51:12] FINAL_MISSING: {"deadline": "2026-11-27T11:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112702021112", "sid": "S00"}
[14:51:12] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.25, "baseline_mean": 0.5, "baseline_stdev": 0.093, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.25, "today_scan_count": 8, "z_score": -2.68}
[14:47:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 475}
[14:43:24] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 472}
```

## 本日残レース: 72件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 84件 締切済
- 通知発射: scan=8 nid / final=5 nid / result=3 nid
- predictions: 5 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 039R | win | 1 | 0.5719 | 2.2 | 1.26 | 200 | scan=- drift=- | 14:28:27 |
| S01_NAKAANA1 | 033R | win | 1 | 0.5703 | 4.8 | 2.74 | 200 | scan=- drift=- | 11:50:46 |
| S00 | 033R | win | 1 | 0.5703 | 4.8 | 2.74 | 300 | scan=- drift=- | 11:50:34 |
| S02_TETSUBAN | 131R | win | 1 | 0.5735 | 2.5 | 1.43 | 200 | scan=2.6 drift=-3.8% | 10:35:36 |
| S00 | 235R | win | 1 | 0.5312 | 4.7 | 2.50 | 300 | scan=6.1 drift=-23.0% | 10:31:14 |
| S01_NAKAANA1 | 206R | win | 1 | 0.5047 | 3.0 | 1.51 | 200 | scan=- drift=- | 17:28:06 |
| S01_NAKAANA1 | 154R | win | 1 | 0.4111 | 4.8 | 1.97 | 200 | scan=4.0 drift=+20.0% | 16:53:40 |
| S02_TETSUBAN | 0312R | win | 1 | 0.4111 | 2.4 | 0.99 | 200 | scan=2.4 drift=+0.0% | 15:59:32 |
| S01_NAKAANA1 | 192R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=- drift=- | 15:45:15 |
| S00 | 1710R | win | 1 | 0.5073 | 9.3 | 4.72 | 300 | scan=4.5 drift=+106.7% | 14:24:12 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 21 | +11.9% | -58.9% | +114.7% | 5 | 2 | 16 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 405.9s |
| **Latency** (scan→final max) | 551.0s |
| **Traffic** (notifications 24h) | 38 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 168 | 0.4720 | 0.3036 | +0.1684 | 🟡+36% | 0.2336 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 55 | 0.4104 | 0.1636 | 0.1923 | 🔴-0.41 | 0.458 |
| S01_NAKAANA1 | win | 77 | 0.4829 | 0.3506 | 0.2442 | 🔴-0.07 | 0.934 |
| S02_TETSUBAN | win | 36 | 0.5427 | 0.4167 | 0.2742 | 🔴-0.13 | 0.928 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 67 | 0.4093 | 0.2985 | 🔴+0.1108 |
| 0.50+ | 94 | 0.5428 | 0.3298 | 🔴+0.2130 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 212 | 0.818 |
| win | <5.0 | ✅learned | 387 | 0.739 |
| win | <10.0 | ✅learned | 160 | 0.449 |
| win | <20.0 | ✅learned | 48 | 0.252 |
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
_auto-generated by claude_snapshot.py at 2026-11-27T15:00:01.737794+09:00_