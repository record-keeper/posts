# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-24T10:50:01.494487+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×37 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×199 (24h)
- 🔴 PSI_DRIFT_DETECTED×37 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×7  [2026-11-24T10:19:29]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×11  [2026-11-24T10:07:16]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×11  [2026-11-24T10:07:16]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×3  [2026-11-24T09:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-24T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=71<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-24T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=40<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-24T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=90<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-24T06:00:19]
- key: `ROI_STAT|S00: n=71 hit%=22.5% hit_CI[Bonf]=[11.6,39.3]% ROI=0.57 ROI_boot95=[0.31,0.88]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-24T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=90 hit%=33.3% hit_CI[Bonf]=[20.9,48.5]% ROI=0.85 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-24T06:00:19]
- key: `ROI_STAT|S02_TETSUBAN: n=40 hit%=40.0% hit_CI[Bonf]=[21.3,62.1]% ROI=1.15 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-11-24T06:00:19]
- key: `ORPHAN_SCAN|266 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-24T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=23 hit%=17.4% ROI=0.77 (コスト 5,000/回収 3,860)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-24T06:00:19]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=38 hit%=44.7% ROI=1.14 (コスト 8,700/回収 9,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-24T06:00:19]
- key: `CALIBRATION_LIVE|bt=win: n=201 pred=0.4776 actual=0.3085 error=+0.1692 (+35%) brier=0.2354 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-24T06:00:19]
- key: `CALIBRATION_LIVE|S00(win): n=71 pred=0.4276 hit=0.2254 cal_err=+0.2022 brier=0.2098 BSS=-0.20 ROI`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-24T06:00:19]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=90 pred=0.4851 hit=0.3333 cal_err=+0.1518 brier=0.2408 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-24T06:00:19]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=40 pred=0.5496 hit=0.4000 cal_err=+0.1496 brier=0.2685 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-24T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=20 pred=0.3198 actual=0.2000 gap=+0.1198`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-24T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=58 pred=0.4470 actual=0.3276 gap=+0.1194`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-24T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.50+: n=114 pred=0.5457 actual=0.3421 gap=+0.2036`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 18.61MB / last modified 2026-11-24T10:48:38.441081+09:00

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
G] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds3f?rno=2&jcd=08&hd=20261124: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-24 10:48:06,251 [INFO] scraper: odds3f: 20/20 parsed
2026-11-24 10:48:17,373 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=2&jcd=08&hd=20261124: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-24 10:48:26,495 [INFO] scraper: odds2t: 30/30 parsed
2026-11-24 10:48:26,496 [INFO] scraper: odds2f: 15/15 parsed
2026-11-24 10:48:36,603 [INFO] scraper: odds_win: 6/6 parsed
2026-11-24 10:48:36,603 [INFO] scraper: fetch_race 08/2: boats=6 odds=191/191
2026-11-24 10:48:36,607 [INFO] predictor: CALIBRATION_MODE=on
2026-11-24 10:48:36,607 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-11-24 10:48:36,611 [INFO] run_cycle: fetched 08/2 [scan]: 156 combos
2026-11-24 10:48:36,783 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-24 10:49:04,606 [INFO] run_cycle: === run_cycle 10:49:04 ===
2026-11-24 10:49:04,606 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-24 10:49:04,606 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-24 10:49:04,637 [INFO] predictor: Models loaded OK
2026-11-24 10:49:33,045 [INFO] scraper: odds3t: 120/120 parsed
2026-11-24 10:49:42,157 [INFO] scraper: odds3f: 20/20 parsed
2026-11-24 10:49:52,323 [INFO] scraper: odds2t: 30/30 parsed
2026-11-24 10:49:52,324 [INFO] scraper: odds2f: 15/15 parsed
2026-11-24 10:50:02,512 [INFO] scraper: odds_win: 5/6 parsed
2026-11-24 10:50:02,512 [INFO] scraper: fetch_race 18/6: boats=6 odds=190/191
2026-11-24 10:50:02,534 [INFO] predictor: CALIBRATION_MODE=on
2026-11-24 10:50:02,535 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-11-24 10:50:02,577 [INFO] run_cycle: fetched 18/6 [final]: 155 combos

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
    "c": 45
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 45
  }
]
```

## Phase別通知記録 (24h)
{'final': 14, 'result': 8, 'scan': 23}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 240
  FINAL_MISSING: 199
  PSI_DRIFT_DETECTED: 37
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 4
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 7 | 2 | 2,100 | 1,380 | -720 | 0.657 |
| S01_NAKAANA1 | 19 | 8 | 3,800 | 3,360 | -440 | 0.884 |
| S02_TETSUBAN | 5 | 2 | 1,000 | 2,160 | +1,160 | 2.16 |

## 直近アラート (24h・新しい順)
```
[10:48:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 481}
[10:46:36] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 169, "n_recent": 31, "psi": 0.616}
[10:46:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 479}
[10:43:21] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 170, "n_recent": 31, "psi": 0.61}
[10:43:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 468}
[10:35:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 461}
[10:31:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 455}
[10:24:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 450}
[10:14:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 429}
[10:12:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 422}
```

## 本日残レース: 157件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 23件 締切済
- 通知発射: scan=1 nid / final=2 nid / result=1 nid
- predictions: 1 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 212R | win | 1 | 0.5334 | 2.8 | 1.49 | 200 | scan=- drift=- | 09:08:14 |
| S01_NAKAANA1 | 074R | win | 1 | 0.5719 | 3.5 | 2.00 | 200 | scan=3.1 drift=+12.9% | 16:34:46 |
| S01_NAKAANA1 | 122R | win | 1 | 0.5123 | 3.3 | 1.69 | 200 | scan=- drift=- | 15:49:13 |
| S01_NAKAANA1 | 135R | win | 1 | 0.5123 | 4.1 | 2.10 | 200 | scan=- drift=- | 12:38:14 |
| S01_NAKAANA1 | 023R | win | 1 | 0.5104 | 3.5 | 1.79 | 200 | scan=3.0 drift=+16.7% | 11:38:24 |
| S00 | 107R | win | 1 | 0.5123 | 24.0 | 12.30 | 300 | scan=- drift=- | 11:34:39 |
| S02_TETSUBAN | 052R | win | 1 | 0.5080 | 2.1 | 1.07 | 200 | scan=- drift=- | 11:00:54 |
| S01_NAKAANA1 | 145R | win | 1 | 0.5476 | 4.9 | 2.68 | 200 | scan=3.9 drift=+25.6% | 10:18:24 |
| S01_NAKAANA1 | 142R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=3.3 drift=+33.3% | 08:59:31 |
| S00 | 142R | win | 1 | 0.4111 | 4.4 | 1.81 | 300 | scan=- drift=- | 08:59:29 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 14 | +2.1% | -25.0% | +33.3% | 4 | 0 | 8 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 368.7s |
| **Latency** (scan→final max) | 611.9s |
| **Traffic** (notifications 24h) | 45 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 199 | 0.4769 | 0.3065 | +0.1703 | 🟡+36% | 0.2357 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 70 | 0.4266 | 0.2286 | 0.2092 | 🔴-0.19 | 0.579 |
| S01_NAKAANA1 | win | 88 | 0.4832 | 0.3182 | 0.2421 | 🔴-0.12 | 0.833 |
| S02_TETSUBAN | win | 41 | 0.5492 | 0.4146 | 0.2673 | 🔴-0.10 | 1.18 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 77 | 0.4133 | 0.2987 | 🔴+0.1146 |
| 0.50+ | 113 | 0.5452 | 0.3363 | 🔴+0.2089 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 209 | 0.818 |
| win | <5.0 | ✅learned | 381 | 0.737 |
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
_auto-generated by claude_snapshot.py at 2026-11-24T10:50:01.494487+09:00_