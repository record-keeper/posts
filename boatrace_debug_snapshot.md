# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-25T12:50:01.595173+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×64 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×11  [2026-05-25T12:39:38]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×4  [2026-05-25T12:35:04]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 STRATEGY_CI_FAIL  ×48  [2026-05-25T12:01:46]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×48  [2026-05-25T12:01:46]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-25T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=190<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-25T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1957 actual=0.1667 gap=+0.0291`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-25T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=12 pred=0.2243 actual=0.3333 gap=-0.1090`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-25T06:00:12]
- key: `ROI_STAT|S02_TETSUBAN: n=44 hit%=45.5% hit_CI[Bonf]=[26.3,66.1]% ROI=0.83 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-25T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=44<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-25T06:00:12]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=44 pred=0.5098 hit=0.4545 cal_err=+0.0553 brier=0.2540 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-25T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=26 pred=0.3234 actual=0.2308 gap=+0.0926`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-25T06:00:12]
- key: `ROI_STAT|S00: n=190 hit%=27.9% hit_CI[Bonf]=[19.6,38.1]% ROI=0.94 ROI_boot95=[0.69,1.21]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-25T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=77 hit%=28.6% hit_CI[Bonf]=[16.4,44.9]% ROI=0.75 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-25T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=77<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-25T06:00:12]
- key: `ORPHAN_SCAN|235 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-25T06:00:12]
- key: `DRIFT_BUCKET|drift ≤-30%: n=49 hit%=32.7% ROI=0.88 (コスト 14,500/回収 12,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-25T06:00:12]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=41 hit%=26.8% ROI=1.14 (コスト 9,600/回収 10,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-25T06:00:12]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=64 hit%=28.1% ROI=0.86 (コスト 15,500/回収 13,320)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-25T06:00:12]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=25 hit%=28.0% ROI=1.11 (コスト 6,100/回収 6,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-25T06:00:12]
- key: `DRIFT_BUCKET|drift ≥+30%: n=37 hit%=18.9% ROI=0.53 (コスト 9,600/回収 5,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.45MB / last modified 2026-05-25T12:49:37.861685+09:00

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
] scraper: odds3t: 120/120 parsed
2026-05-25 12:49:18,213 [INFO] scraper: odds3f: 20/20 parsed
2026-05-25 12:49:19,525 [INFO] scraper: odds2t: 29/30 parsed
2026-05-25 12:49:19,526 [INFO] scraper: odds2f: 12/15 parsed
2026-05-25 12:49:20,647 [INFO] scraper: odds_win: 3/6 parsed
2026-05-25 12:49:20,647 [INFO] scraper: fetch_race 09/6: boats=6 odds=184/191
2026-05-25 12:49:20,656 [INFO] predictor: CALIBRATION_MODE=on
2026-05-25 12:49:20,657 [INFO] predictor: combos: {'win': 3, '2t': 29, '3t': 120}
2026-05-25 12:49:20,664 [INFO] run_cycle: fetched 09/6 [final]: 152 combos
2026-05-25 12:49:24,182 [INFO] scraper: odds3t: 120/120 parsed
2026-05-25 12:49:25,312 [INFO] scraper: odds3f: 20/20 parsed
2026-05-25 12:49:26,438 [INFO] scraper: odds2t: 29/30 parsed
2026-05-25 12:49:26,439 [INFO] scraper: odds2f: 14/15 parsed
2026-05-25 12:49:27,610 [INFO] scraper: odds_win: 4/6 parsed
2026-05-25 12:49:27,610 [INFO] scraper: fetch_race 10/10: boats=6 odds=187/191
2026-05-25 12:49:27,620 [INFO] predictor: CALIBRATION_MODE=on
2026-05-25 12:49:27,620 [INFO] predictor: combos: {'win': 4, '2t': 29, '3t': 120}
2026-05-25 12:49:27,628 [INFO] run_cycle: fetched 10/10 [scan]: 153 combos
2026-05-25 12:49:31,493 [INFO] scraper: odds3t: 120/120 parsed
2026-05-25 12:49:32,654 [INFO] scraper: odds3f: 20/20 parsed
2026-05-25 12:49:33,778 [INFO] scraper: odds2t: 30/30 parsed
2026-05-25 12:49:33,779 [INFO] scraper: odds2f: 13/15 parsed
2026-05-25 12:49:34,932 [INFO] scraper: odds_win: 6/6 parsed
2026-05-25 12:49:34,933 [INFO] scraper: fetch_race 17/5: boats=6 odds=189/191
2026-05-25 12:49:34,950 [INFO] predictor: CALIBRATION_MODE=on
2026-05-25 12:49:34,951 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-25 12:49:34,962 [INFO] run_cycle: fetched 17/5 [scan]: 156 combos
2026-05-25 12:49:37,628 [WARNING] scraper: beforeinfo parse failed: jcd=03 rno=5
2026-05-25 12:49:37,628 [WARNING] run_cycle: fetch None: 03/5
2026-05-25 12:49:37,628 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 55
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 55
  }
]
```

## Phase別通知記録 (24h)
{'final': 19, 'result': 10, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 210
  FINAL_MISSING: 64
  KS_ODDS_DRIFT: 40
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 13
  ANOMALY_BET_VOLUME_SPIKE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 34 | 11 | 10,200 | 13,320 | +3,120 | 1.306 |
| S01_NAKAANA1 | 34 | 7 | 6,800 | 5,080 | -1,720 | 0.747 |
| S02_TETSUBAN | 13 | 5 | 2,600 | 1,540 | -1,060 | 0.592 |

## 直近アラート (24h・新しい順)
```
[12:47:21] FINAL_MISSING: {"deadline": "2026-05-25T11:17:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052523071117", "sid": "S00"}
[12:45:47] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.00813, "ks_stat": 0.211}
[12:37:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1089}
[12:36:06] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.007172, "ks_stat": 0.213}
[12:36:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1104}
[12:35:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1126}
[12:32:24] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.005126, "ks_stat": 0.219}
[12:32:24] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.341, "baseline_mean": 0.887, "baseline_stdev": 0.069, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.545, "today_scan_count": 11, "z_score": -4.95}
[12:27:30] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.432, "baseline_mean": 0.887, "baseline_stdev": 0.069, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.455, "today_scan_count": 11, "z_score": -6.27}
[12:26:29] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.387, "baseline_mean": 0.887, "baseline_stdev": 0.069, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 10, "z_score": -5.61}
```

## 本日残レース: 90件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 54件 締切済
- 通知発射: scan=11 nid / final=6 nid / result=3 nid
- predictions: 5 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 7件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 034R | win | 1 | 0.0295 | 5.9 | 0.17 | 300 | scan=14.2 drift=-58.5% | 12:32:22 |
| S01_NAKAANA1 | 132R | win | 1 | 0.4111 | 4.8 | 1.97 | 200 | scan=4.1 drift=+17.1% | 11:07:21 |
| S00 | 132R | win | 1 | 0.4111 | 4.8 | 1.97 | 300 | scan=4.1 drift=+17.1% | 11:07:21 |
| S01_NAKAANA1 | 236R | win | 1 | 0.5174 | 3.7 | 1.91 | 200 | scan=- drift=- | 10:43:20 |
| S00 | 102R | win | 1 | 0.0918 | 5.6 | 0.51 | 300 | scan=5.4 drift=+3.7% | 09:02:23 |
| S00 | 246R | win | 1 | 0.0295 | 10.3 | 0.30 | 300 | scan=4.0 drift=+157.5% | 17:47:21 |
| S01_NAKAANA1 | 244R | win | 1 | 0.5476 | 3.9 | 2.14 | 200 | scan=3.5 drift=+11.4% | 16:57:21 |
| S00 | 243R | win | 1 | 0.5123 | 6.9 | 3.53 | 300 | scan=6.8 drift=+1.5% | 16:27:22 |
| S01_NAKAANA1 | 013R | win | 1 | 0.5334 | 3.1 | 1.65 | 200 | scan=3.6 drift=-13.9% | 16:24:22 |
| S01_NAKAANA1 | 1010R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=- drift=- | 12:52:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 52 | +1.9% | -78.6% | +157.5% | 19 | 10 | 38 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 508.5s |
| **Latency** (scan→final max) | 628.9s |
| **Traffic** (notifications 24h) | 55 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 308 | 0.4564 | 0.3019 | +0.1545 | 🟡+34% | 0.2323 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 185 | 0.4323 | 0.2757 | 0.2229 | 🔴-0.12 | 0.943 |
| S01_NAKAANA1 | win | 79 | 0.4832 | 0.2785 | 0.2423 | 🔴-0.21 | 0.728 |
| S02_TETSUBAN | win | 44 | 0.5098 | 0.4545 | 0.2540 | 🔴-0.02 | 0.827 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 15 | 0.0082 | 0.0667 | 🔴-0.0585 |
| 0.15-0.20 | 5 | 0.1957 | 0.2000 | ✅-0.0043 |
| 0.20-0.30 | 12 | 0.2243 | 0.3333 | 🔴-0.1090 |
| 0.30-0.50 | 137 | 0.4184 | 0.2482 | 🔴+0.1702 |
| 0.50+ | 146 | 0.5403 | 0.3699 | 🔴+0.1705 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 20 | 0.744 |
| win | <5.0 | ✅learned | 38 | 0.802 |
| win | <10.0 | ✅learned | 34 | 0.547 |
| win | <20.0 | ✅learned | 11 | 0.193 |
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
_auto-generated by claude_snapshot.py at 2026-05-25T12:50:01.595173+09:00_