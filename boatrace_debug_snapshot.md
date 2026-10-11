# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-11T15:40:01.487295+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×49 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×4 (24h)
- 🟡 LARGE_ODDS_DRIFT×3 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×36  [2026-10-11T15:04:38]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×20  [2026-10-11T13:23:55]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×24  [2026-10-11T11:47:22]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-10-11T10:00:16]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-11T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=76<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-11T06:00:17]
- key: `ORPHAN_SCAN|169 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-11T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-11T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S00: n=166<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-10-11T06:00:17]
- key: `ROI_STAT|S00: n=166 hit%=25.9% hit_CI[Bonf]=[17.4,36.7]% ROI=0.72 ROI_boot95=[0.50,0.95]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-11T06:00:17]
- key: `ROI_STAT|S01_NAKAANA1: n=163 hit%=34.4% hit_CI[Bonf]=[24.6,45.6]% ROI=1.05 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-11T06:00:17]
- key: `ROI_STAT|S02_TETSUBAN: n=76 hit%=51.3% hit_CI[Bonf]=[35.5,66.9]% ROI=0.91 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-11T06:00:17]
- key: `DRIFT_BUCKET|drift ≤-30%: n=29 hit%=41.4% ROI=1.17 (コスト 8,400/回収 9,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-11T06:00:17]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=50 hit%=30.0% ROI=0.74 (コスト 11,800/回収 8,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-11T06:00:17]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=87 hit%=34.5% ROI=0.91 (コスト 19,800/回収 18,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-11T06:00:17]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=50 hit%=40.0% ROI=1.00 (コスト 11,800/回収 11,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-11T06:00:17]
- key: `DRIFT_BUCKET|drift ≥+30%: n=41 hit%=22.0% ROI=0.67 (コスト 10,800/回収 7,260)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-11T06:00:17]
- key: `CALIBRATION_LIVE|bt=win: n=405 pred=0.4826 actual=0.3407 error=+0.1419 (+29%) brier=0.2522 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-11T06:00:17]
- key: `CALIBRATION_LIVE|S00(win): n=166 pred=0.4543 hit=0.2590 cal_err=+0.1952 brier=0.2550 BSS=-0.33 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-11T06:00:17]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=163 pred=0.4924 hit=0.3436 cal_err=+0.1488 brier=0.2475 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-11T06:00:17]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=76 pred=0.5237 hit=0.5132 cal_err=+0.0106 brier=0.2563 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 15.46MB / last modified 2026-10-11T15:39:33.229815+09:00

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
2026-10-11 15:39:04,123 [INFO] predictor: Models loaded OK
2026-10-11 15:39:15,495 [INFO] scraper: odds3t: 120/120 parsed
2026-10-11 15:39:16,731 [INFO] scraper: odds3f: 20/20 parsed
2026-10-11 15:39:17,897 [INFO] scraper: odds2t: 30/30 parsed
2026-10-11 15:39:17,898 [INFO] scraper: odds2f: 15/15 parsed
2026-10-11 15:39:18,997 [INFO] scraper: odds_win: 6/6 parsed
2026-10-11 15:39:18,997 [INFO] scraper: fetch_race 09/11: boats=6 odds=191/191
2026-10-11 15:39:19,000 [INFO] predictor: CALIBRATION_MODE=on
2026-10-11 15:39:19,000 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-11 15:39:19,004 [INFO] run_cycle: fetched 09/11 [final]: 156 combos
2026-10-11 15:39:22,526 [INFO] scraper: odds3t: 120/120 parsed
2026-10-11 15:39:23,728 [INFO] scraper: odds3f: 20/20 parsed
2026-10-11 15:39:24,807 [INFO] scraper: odds2t: 30/30 parsed
2026-10-11 15:39:24,809 [INFO] scraper: odds2f: 15/15 parsed
2026-10-11 15:39:25,923 [INFO] scraper: odds_win: 6/6 parsed
2026-10-11 15:39:25,923 [INFO] scraper: fetch_race 12/2: boats=6 odds=191/191
2026-10-11 15:39:25,926 [INFO] predictor: CALIBRATION_MODE=on
2026-10-11 15:39:25,926 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-11 15:39:25,930 [INFO] run_cycle: fetched 12/2 [scan]: 156 combos
2026-10-11 15:39:29,530 [INFO] scraper: odds3t: 120/120 parsed
2026-10-11 15:39:30,670 [INFO] scraper: odds3f: 20/20 parsed
2026-10-11 15:39:31,786 [INFO] scraper: odds2t: 30/30 parsed
2026-10-11 15:39:31,787 [INFO] scraper: odds2f: 15/15 parsed
2026-10-11 15:39:32,916 [INFO] scraper: odds_win: 5/6 parsed
2026-10-11 15:39:32,917 [INFO] scraper: fetch_race 15/2: boats=6 odds=190/191
2026-10-11 15:39:32,919 [INFO] predictor: CALIBRATION_MODE=on
2026-10-11 15:39:32,919 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-10-11 15:39:32,923 [INFO] run_cycle: fetched 15/2 [scan]: 155 combos
2026-10-11 15:39:33,045 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 72
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 72
  }
]
```

## Phase別通知記録 (24h)
{'final': 27, 'result': 14, 'scan': 31}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 122
  FINAL_MISSING: 49
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 4
  PSI_DRIFT_DETECTED: 4
  LARGE_ODDS_DRIFT: 3
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 33 | 14 | 9,900 | 10,890 | +990 | 1.1 |
| S01_NAKAANA1 | 37 | 17 | 7,400 | 8,620 | +1,220 | 1.165 |
| S02_TETSUBAN | 17 | 9 | 3,400 | 3,300 | -100 | 0.971 |

## 直近アラート (24h・新しい順)
```
[15:31:15] FINAL_MISSING: {"deadline": "2026-10-11T12:00:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101106031200", "sid": "S00"}
[15:28:31] FINAL_MISSING: {"deadline": "2026-10-11T12:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101122051258", "sid": "S00"}
[15:22:03] FINAL_MISSING: {"deadline": "2026-10-11T11:51:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101116031151", "sid": "S00"}
[15:04:36] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[14:31:03] FINAL_MISSING: {"deadline": "2026-10-11T12:00:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101106031200", "sid": "S00"}
[14:28:04] FINAL_MISSING: {"deadline": "2026-10-11T12:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101122051258", "sid": "S00"}
[14:21:30] FINAL_MISSING: {"deadline": "2026-10-11T11:51:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101116031151", "sid": "S00"}
[14:03:38] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:40:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1096}
[13:38:31] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1087}
```

## 本日残レース: 58件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 98件 締切済
- 通知発射: scan=13 nid / final=14 nid / result=7 nid
- predictions: 8 / うち結果DB記録済: 7
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 151R | win | 1 | 0.5891 | 5.0 | 2.95 | 300 | scan=- drift=- | 15:17:26 |
| S00 | 227R | win | 1 | 0.5476 | 6.0 | 3.29 | 300 | scan=5.2 drift=+15.4% | 13:51:18 |
| S01_NAKAANA1 | 066R | win | 1 | 0.4480 | 4.1 | 1.84 | 200 | scan=4.0 drift=+2.5% | 13:31:30 |
| S02_TETSUBAN | 036R | win | 1 | 0.5891 | 2.5 | 1.47 | 200 | scan=- drift=- | 13:27:31 |
| S02_TETSUBAN | 097R | win | 1 | 0.5719 | 2.2 | 1.26 | 200 | scan=2.1 drift=+4.8% | 13:24:30 |
| S02_TETSUBAN | 096R | win | 1 | 0.5123 | 2.9 | 1.49 | 200 | scan=- drift=- | 12:53:18 |
| S01_NAKAANA1 | 064R | win | 1 | 0.5891 | 4.9 | 2.89 | 200 | scan=4.3 drift=+14.0% | 12:36:19 |
| S00 | 223R | win | 1 | 0.5174 | 19.2 | 9.93 | 300 | scan=4.5 drift=+326.7% | 12:01:29 |
| S02_TETSUBAN | 076R | win | 1 | 0.4989 | 2.1 | 1.05 | 200 | scan=- drift=- | 17:41:18 |
| S01_NAKAANA1 | 014R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=3.7 drift=+0.0% | 16:50:44 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 54 | +10.4% | -68.9% | +326.7% | 16 | 7 | 37 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 478.8s |
| **Latency** (scan→final max) | 610.9s |
| **Traffic** (notifications 24h) | 72 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 408 | 0.4837 | 0.3431 | +0.1405 | 🟡+29% | 0.2523 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 168 | 0.4552 | 0.2560 | 0.2553 | 🔴-0.34 | 0.707 |
| S01_NAKAANA1 | win | 162 | 0.4936 | 0.3457 | 0.2487 | 🔴-0.10 | 1.057 |
| S02_TETSUBAN | win | 78 | 0.5244 | 0.5256 | 0.2534 | 🔴-0.02 | 0.936 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 149 | 0.4205 | 0.3087 | 🔴+0.1118 |
| 0.50+ | 244 | 0.5433 | 0.3648 | 🔴+0.1785 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 176 | 0.772 |
| win | <5.0 | ✅learned | 315 | 0.759 |
| win | <10.0 | ✅learned | 138 | 0.461 |
| win | <20.0 | ✅learned | 39 | 0.243 |
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
_auto-generated by claude_snapshot.py at 2026-10-11T15:40:01.487295+09:00_