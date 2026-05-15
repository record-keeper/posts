# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-15T12:30:02.485366+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×30 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×75 (24h)
- 🔴 PSI_DRIFT_DETECTED×30 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×27  [2026-05-15T12:03:26]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×27  [2026-05-15T12:03:26]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×27  [2026-05-15T12:03:26]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×5  [2026-05-15T11:24:40]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-15T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=13 pred=0.0030 actual=0.0769 gap=-0.0739`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-15T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1907 actual=0.1429 gap=+0.0479`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-15T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2234 actual=0.3000 gap=-0.0766`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-15T06:00:19]
- key: `ROI_STAT|S00: n=183 hit%=25.7% hit_CI[Bonf]=[17.6,35.9]% ROI=0.86 ROI_boot95=[0.62,1.12]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-15T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=183<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-15T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=35 hit%=40.0% hit_CI[Bonf]=[20.4,63.5]% ROI=0.80 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-15T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=35<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-15T06:00:19]
- key: `ORPHAN_SCAN|220 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-15T06:00:19]
- key: `DRIFT_BUCKET|drift ≤-30%: n=41 hit%=22.0% ROI=0.60 (コスト 12,100/回収 7,290)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-15T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=31 hit%=32.3% ROI=1.48 (コスト 7,500/回収 11,070)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-15T06:00:19]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=49 hit%=30.6% ROI=1.03 (コスト 12,400/回収 12,720)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-15T06:00:19]
- key: `DRIFT_BUCKET|drift ≥+30%: n=33 hit%=21.2% ROI=0.60 (コスト 8,800/回収 5,280)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-15T06:00:19]
- key: `CALIBRATION_LIVE|bt=win: n=242 pred=0.4545 actual=0.3017 error=+0.1529 (+34%) brier=0.2324 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-15T06:00:19]
- key: `CALIBRATION_LIVE|S00(win): n=183 pred=0.4382 hit=0.2568 cal_err=+0.1814 brier=0.2283 BSS=-0.20 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-15T06:00:19]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=35 pred=0.4969 hit=0.4000 cal_err=+0.0969 brier=0.2378 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-15T06:00:19]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=24 pred=0.5166 hit=0.5000 cal_err=+0.0166 brier=0.2559 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 2.76MB / last modified 2026-05-15T12:30:04.449791+09:00

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
by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-15 12:29:05,525 [INFO] predictor: Models loaded OK
2026-05-15 12:29:18,140 [INFO] scraper: odds3t: 120/120 parsed
2026-05-15 12:29:19,218 [INFO] scraper: odds3f: 20/20 parsed
2026-05-15 12:29:20,308 [INFO] scraper: odds2t: 28/30 parsed
2026-05-15 12:29:20,309 [INFO] scraper: odds2f: 14/15 parsed
2026-05-15 12:29:21,384 [INFO] scraper: odds_win: 3/6 parsed
2026-05-15 12:29:21,384 [INFO] scraper: fetch_race 08/5: boats=6 odds=185/191
2026-05-15 12:29:21,396 [INFO] predictor: CALIBRATION_MODE=on
2026-05-15 12:29:21,396 [INFO] predictor: combos: {'win': 3, '2t': 28, '3t': 120}
2026-05-15 12:29:21,403 [INFO] run_cycle: fetched 08/5 [final]: 151 combos
2026-05-15 12:29:25,089 [INFO] scraper: odds3t: 120/120 parsed
2026-05-15 12:29:26,259 [INFO] scraper: odds3f: 20/20 parsed
2026-05-15 12:29:27,359 [INFO] scraper: odds2t: 30/30 parsed
2026-05-15 12:29:27,361 [INFO] scraper: odds2f: 15/15 parsed
2026-05-15 12:29:28,461 [INFO] scraper: odds_win: 6/6 parsed
2026-05-15 12:29:28,462 [INFO] scraper: fetch_race 16/4: boats=6 odds=191/191
2026-05-15 12:29:28,471 [INFO] predictor: CALIBRATION_MODE=on
2026-05-15 12:29:28,471 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-15 12:29:28,479 [INFO] run_cycle: fetched 16/4 [scan]: 156 combos
2026-05-15 12:29:31,991 [INFO] scraper: odds3t: 120/120 parsed
2026-05-15 12:29:33,075 [INFO] scraper: odds3f: 20/20 parsed
2026-05-15 12:29:34,227 [INFO] scraper: odds2t: 30/30 parsed
2026-05-15 12:29:34,228 [INFO] scraper: odds2f: 15/15 parsed
2026-05-15 12:29:35,422 [INFO] scraper: odds_win: 6/6 parsed
2026-05-15 12:29:35,422 [INFO] scraper: fetch_race 21/5: boats=6 odds=191/191
2026-05-15 12:29:35,430 [INFO] predictor: CALIBRATION_MODE=on
2026-05-15 12:29:35,430 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-15 12:29:35,438 [INFO] run_cycle: fetched 21/5 [scan]: 156 combos
2026-05-15 12:29:35,555 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 68
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 68
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 16, 'scan': 27}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 75
  ANOMALY_SCRAPER_FAILURE_BURST: 43
  PSI_DRIFT_DETECTED: 30
  KS_ODDS_DRIFT: 29
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 4
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 53 | 14 | 15,900 | 12,570 | -3,330 | 0.791 |
| S01_NAKAANA1 | 36 | 14 | 7,200 | 5,620 | -1,580 | 0.781 |
| S02_TETSUBAN | 25 | 13 | 5,000 | 5,000 | +0 | 1.0 |
| S04_SELL_3T | 12 | 1 | 1,200 | 740 | -460 | 0.617 |

## 直近アラート (24h・新しい順)
```
[12:29:35] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.501}
[12:01:28] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:00:33] FINAL_MISSING: {"deadline": "2026-05-15T10:30:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051510051030", "sid": "S00"}
[11:56:30] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 133, "n_recent": 114, "psi": 0.401}
[11:54:32] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.498}
[11:54:32] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 133, "n_recent": 113, "psi": 0.404}
[11:41:39] FINAL_MISSING: {"deadline": "2026-05-15T09:10:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051510020910", "sid": "S00"}
[11:37:27] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.504}
[11:37:27] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 133, "n_recent": 112, "psi": 0.407}
[11:29:30] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.501}
```

## 本日残レース: 112件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 44件 締切済
- 通知発射: scan=6 nid / final=6 nid / result=5 nid
- predictions: 5 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 108R | win | 1 | 0.4111 | 3.4 | 1.40 | 200 | scan=4.1 drift=-17.1% | 11:56:21 |
| S00 | 134R | win | 1 | 0.4111 | 9.5 | 3.91 | 300 | scan=- drift=- | 11:54:21 |
| S02_TETSUBAN | 213R | win | 1 | 0.4111 | 2.0 | 0.82 | 200 | scan=- drift=- | 11:37:22 |
| S00 | 133R | win | 1 | 0.1371 | 5.5 | 0.75 | 300 | scan=23.2 drift=-76.3% | 11:29:20 |
| S00 | 131R | win | 1 | 0.4111 | 9.7 | 3.99 | 300 | scan=12.7 drift=-23.6% | 10:34:33 |
| S02_TETSUBAN | 0711R | win | 1 | 0.5990 | 2.2 | 1.32 | 200 | scan=2.2 drift=+0.0% | 20:08:46 |
| S02_TETSUBAN | 079R | win | 1 | 0.5123 | 2.0 | 1.02 | 200 | scan=- drift=- | 19:15:21 |
| S01_NAKAANA1 | 076R | win | 1 | 0.5123 | 4.0 | 2.05 | 200 | scan=4.6 drift=-13.0% | 17:59:22 |
| S01_NAKAANA1 | 074R | win | 1 | 0.5735 | 4.6 | 2.64 | 200 | scan=3.3 drift=+39.4% | 17:09:32 |
| S00 | 0410R | win | 1 | 0.5334 | 14.1 | 7.52 | 300 | scan=30.0 drift=-53.0% | 16:34:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| 3t | 12 | +11.6% | -41.4% | +75.7% | 5 | 1 | 9 |
| win | 75 | +2.1% | -76.3% | +522.0% | 31 | 17 | 49 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 479.4s |
| **Latency** (scan→final max) | 608.8s |
| **Traffic** (notifications 24h) | 68 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 247 | 0.4525 | 0.2996 | +0.1529 | 🟡+34% | 0.2312 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 186 | 0.4363 | 0.2527 | 0.2265 | 🔴-0.20 | 0.845 |
| S01_NAKAANA1 | win | 36 | 0.4945 | 0.3889 | 0.2359 | ✅+0.01 | 0.781 |
| S02_TETSUBAN | win | 25 | 0.5124 | 0.5200 | 0.2595 | 🔴-0.04 | 1.0 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 13 | 0.0030 | 0.0769 | 🔴-0.0739 |
| 0.15-0.20 | 7 | 0.1907 | 0.1429 | ✅+0.0479 |
| 0.20-0.30 | 10 | 0.2234 | 0.3000 | 🔴-0.0766 |
| 0.30-0.50 | 114 | 0.4254 | 0.2632 | 🔴+0.1623 |
| 0.50+ | 109 | 0.5410 | 0.3578 | 🔴+0.1832 |

## Settlement Ratio データ品質

- 学習済み: 3バンド / fallback: 14バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 13 | 0.8 |
| win | <5.0 | ✅learned | 27 | 0.718 |
| win | <10.0 | ✅learned | 25 | 0.564 |
| win | <20.0 | ⚠️fallback | 9 | 0.22 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-05-15T12:30:02.485366+09:00_