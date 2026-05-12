# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-12T16:50:01.720595+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×47 (24h)
- 🔴 PSI_DRIFT_DETECTED×42 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×39  [2026-05-12T16:09:06]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×45  [2026-05-12T16:03:28]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×45  [2026-05-12T16:03:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×45  [2026-05-12T16:03:28]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-12T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2241 actual=0.3333 gap=-0.1093`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-12T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1899 actual=0.1667 gap=+0.0232`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-12T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=13 pred=0.0030 actual=0.0769 gap=-0.0739`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-12T06:00:08]
- key: `ROI_STAT|S00: n=157 hit%=25.5% hit_CI[Bonf]=[16.9,36.6]% ROI=0.87 ROI_boot95=[0.61,1.16]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-12T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S00: n=157<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-12T06:00:08]
- key: `ORPHAN_SCAN|195 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-12T06:00:08]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=17.1% ROI=0.44 (コスト 10,300/回収 4,560)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-12T06:00:08]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=26 hit%=30.8% ROI=1.52 (コスト 6,400/回収 9,720)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-12T06:00:08]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=34 hit%=29.4% ROI=1.17 (コスト 8,700/回収 10,170)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-12T06:00:08]
- key: `DRIFT_BUCKET|drift ≥+30%: n=27 hit%=22.2% ROI=0.64 (コスト 7,200/回収 4,600)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-12T06:00:08]
- key: `CALIBRATION_LIVE|bt=win: n=184 pred=0.4449 actual=0.2772 error=+0.1677 (+38%) brier=0.2331 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-12T06:00:08]
- key: `CALIBRATION_LIVE|S00(win): n=157 pred=0.4363 hit=0.2548 cal_err=+0.1816 brier=0.2298 BSS=-0.21 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-12T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=16 pred=0.3290 actual=0.1875 gap=+0.1415`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-12T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=72 pred=0.4463 actual=0.2639 gap=+0.1824`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-12T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.50+: n=76 pred=0.5376 actual=0.3158 gap=+0.2218`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-12T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 2.59MB / last modified 2026-05-12T16:49:06.059628+09:00

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
, port=443): Read timed out. (read timeout=10), retry in 1s
2026-05-12 16:48:27,952 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=16&hd=20260512: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-05-12 16:48:41,516 [INFO] scraper: odds3t: 120/120 parsed
2026-05-12 16:48:42,607 [INFO] scraper: odds3f: 20/20 parsed
2026-05-12 16:48:43,721 [INFO] scraper: odds2t: 30/30 parsed
2026-05-12 16:48:43,722 [INFO] scraper: odds2f: 15/15 parsed
2026-05-12 16:48:44,987 [INFO] scraper: odds_win: 6/6 parsed
2026-05-12 16:48:44,987 [INFO] scraper: fetch_race 16/12: boats=6 odds=191/191
2026-05-12 16:48:44,998 [INFO] predictor: CALIBRATION_MODE=on
2026-05-12 16:48:44,998 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-12 16:48:45,006 [INFO] run_cycle: fetched 16/12 [final]: 156 combos
2026-05-12 16:48:48,452 [INFO] scraper: odds3t: 120/120 parsed
2026-05-12 16:48:49,571 [INFO] scraper: odds3f: 20/20 parsed
2026-05-12 16:48:50,712 [INFO] scraper: odds2t: 29/30 parsed
2026-05-12 16:48:50,713 [INFO] scraper: odds2f: 14/15 parsed
2026-05-12 16:48:51,821 [INFO] scraper: odds_win: 3/6 parsed
2026-05-12 16:48:51,822 [INFO] scraper: fetch_race 22/10: boats=6 odds=186/191
2026-05-12 16:48:51,828 [INFO] predictor: CALIBRATION_MODE=on
2026-05-12 16:48:51,828 [INFO] predictor: combos: {'win': 3, '2t': 29, '3t': 120}
2026-05-12 16:48:51,836 [INFO] run_cycle: fetched 22/10 [scan]: 152 combos
2026-05-12 16:48:52,037 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-12 16:49:05,432 [INFO] run_cycle: === run_cycle 16:49:05 ===
2026-05-12 16:49:05,432 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-12 16:49:05,432 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-12 16:49:05,500 [INFO] predictor: Models loaded OK
2026-05-12 16:49:05,904 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 88
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 88
  }
]
```

## Phase別通知記録 (24h)
{'final': 34, 'result': 20, 'scan': 34}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 138
  FINAL_MISSING: 47
  PSI_DRIFT_DETECTED: 42
  KS_ODDS_DRIFT: 39
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 7
  LARGE_ODDS_DRIFT: 2
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 12 | 12,600 | 10,470 | -2,130 | 0.831 |
| S01_NAKAANA1 | 21 | 8 | 4,200 | 3,300 | -900 | 0.786 |
| S02_TETSUBAN | 16 | 9 | 3,200 | 3,700 | +500 | 1.156 |
| S04_SELL_3T | 12 | 1 | 1,200 | 740 | -460 | 0.617 |

## 直近アラート (24h・新しい順)
```
[16:49:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1101}
[16:48:52] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1097}
[16:46:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1128}
[16:45:42] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1124}
[16:43:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1155}
[16:42:25] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.43}
[16:42:25] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 124, "n_recent": 79, "psi": 0.404}
[16:42:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1156}
[16:41:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1147}
[16:40:08] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1161}
```

## 本日残レース: 41件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 127件 締切済
- 通知発射: scan=25 nid / final=25 nid / result=15 nid
- predictions: 19 / うち結果DB記録済: 17
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 7件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 123R | win | 1 | 0.5891 | 3.8 | 2.24 | 200 | scan=3.9 drift=-2.6% | 16:42:23 |
| S00 | 203R | win | 1 | 0.5334 | 25.5 | 13.60 | 300 | scan=4.1 drift=+522.0% | 16:33:53 |
| S01_NAKAANA1 | 049R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=3.5 drift=+0.0% | 16:00:24 |
| S02_TETSUBAN | 072R | win | 1 | 0.5334 | 2.7 | 1.44 | 200 | scan=2.4 drift=+12.5% | 15:58:45 |
| S00 | 202R | win | 1 | 0.3177 | 4.7 | 1.49 | 300 | scan=- drift=- | 15:57:45 |
| S01_NAKAANA1 | 202R | win | 1 | 0.3177 | 3.3 | 1.05 | 200 | scan=- drift=- | 15:56:19 |
| S00 | 048R | win | 1 | 0.5174 | 11.5 | 5.95 | 300 | scan=22.5 drift=-48.9% | 15:26:56 |
| S01_NAKAANA1 | 201R | win | 1 | 0.5334 | 4.3 | 2.29 | 200 | scan=3.5 drift=+22.9% | 15:23:21 |
| S00 | 201R | win | 1 | 0.5334 | 4.3 | 2.29 | 300 | scan=4.3 drift=+0.0% | 15:23:20 |
| S01_NAKAANA1 | 011R | win | 1 | 0.5334 | 3.5 | 1.87 | 200 | scan=4.0 drift=-12.5% | 15:20:41 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| 3t | 12 | +11.6% | -41.4% | +75.7% | 5 | 1 | 9 |
| win | 56 | +4.9% | -75.4% | +522.0% | 24 | 15 | 39 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 475.6s |
| **Latency** (scan→final max) | 650.7s |
| **Traffic** (notifications 24h) | 88 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,700円 used |
| **Saturation** (S01_NAKAANA1) | 1,400円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 201 | 0.4460 | 0.2886 | +0.1575 | 🟡+35% | 0.2307 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 165 | 0.4351 | 0.2485 | 0.2276 | 🔴-0.22 | 0.844 |
| S01_NAKAANA1 | win | 20 | 0.4897 | 0.4000 | 0.2359 | ✅+0.02 | 0.825 |
| S02_TETSUBAN | win | 16 | 0.5037 | 0.5625 | 0.2566 | 🔴-0.04 | 1.156 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 13 | 0.0030 | 0.0769 | 🔴-0.0739 |
| 0.15-0.20 | 7 | 0.1907 | 0.1429 | ✅+0.0479 |
| 0.20-0.30 | 10 | 0.2234 | 0.3000 | 🔴-0.0766 |
| 0.30-0.50 | 93 | 0.4241 | 0.2473 | 🔴+0.1768 |
| 0.50+ | 86 | 0.5370 | 0.3488 | 🔴+0.1882 |

## Settlement Ratio データ品質

- 学習済み: 2バンド / fallback: 15バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 9 | 0.4 |
| win | <5.0 | ✅learned | 15 | 0.832 |
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
_auto-generated by claude_snapshot.py at 2026-05-12T16:50:01.720595+09:00_