# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-18T14:10:02.402884+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×42 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×54 (24h)
- 🔴 PSI_DRIFT_DETECTED×42 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×6  [2026-06-18T14:04:22]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×6  [2026-06-18T14:04:22]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×38  [2026-06-18T13:32:28]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×44  [2026-06-18T10:00:25]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-18T06:00:20]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=77<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-18T06:00:20]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1835 actual=0.2000 gap=-0.0165`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-18T06:00:20]
- key: `ORPHAN_SCAN|137 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-18T06:00:20]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=21 pred=0.3200 actual=0.3333 gap=-0.0134`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-18T06:00:20]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=26.5% ROI=0.80 (コスト 9,900/回収 7,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-18T06:00:20]
- key: `DRIFT_BUCKET|drift ≥+30%: n=27 hit%=18.5% ROI=0.40 (コスト 7,600/回収 3,010)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-06-18T06:00:20]
- key: `ROI_STAT|S00: n=147 hit%=27.9% hit_CI[Bonf]=[18.6,39.5]% ROI=0.84 ROI_boot95=[0.59,1.13]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-18T06:00:20]
- key: `INSUFFICIENT_SAMPLE|S00: n=147<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-18T06:00:20]
- key: `ROI_STAT|S01_NAKAANA1: n=135 hit%=28.9% hit_CI[Bonf]=[19.1,41.1]% ROI=0.83 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-18T06:00:20]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=135<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-18T06:00:20]
- key: `ROI_STAT|S02_TETSUBAN: n=77 hit%=36.4% hit_CI[Bonf]=[22.6,52.8]% ROI=0.59 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-18T06:00:20]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=32 hit%=12.5% ROI=0.23 (コスト 7,200/回収 1,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-18T06:00:20]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=68 hit%=29.4% ROI=0.66 (コスト 16,000/回収 10,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-18T06:00:20]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=39 hit%=23.1% ROI=1.04 (コスト 9,000/回収 9,350)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-18T06:00:20]
- key: `CALIBRATION_LIVE|bt=win: n=359 pred=0.4710 actual=0.3008 error=+0.1702 (+36%) brier=0.2377 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-18T06:00:20]
- key: `CALIBRATION_LIVE|S00(win): n=147 pred=0.4243 hit=0.2789 cal_err=+0.1454 brier=0.2167 BSS=-0.08 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.32MB / last modified 2026-06-18T14:09:41.848170+09:00

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
O] scraper: odds3f: 20/20 parsed
2026-06-18 14:08:19,447 [INFO] scraper: odds2t: 30/30 parsed
2026-06-18 14:08:19,449 [INFO] scraper: odds2f: 15/15 parsed
2026-06-18 14:08:20,566 [INFO] scraper: odds_win: 6/6 parsed
2026-06-18 14:08:20,566 [INFO] scraper: fetch_race 08/8: boats=6 odds=191/191
2026-06-18 14:08:20,578 [INFO] predictor: CALIBRATION_MODE=on
2026-06-18 14:08:20,579 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-18 14:08:20,587 [INFO] run_cycle: fetched 08/8 [final]: 156 combos
2026-06-18 14:08:20,867 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-18 14:09:06,032 [INFO] run_cycle: === run_cycle 14:09:06 ===
2026-06-18 14:09:06,032 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-18 14:09:06,032 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-18 14:09:06,136 [INFO] predictor: Models loaded OK
2026-06-18 14:09:17,208 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=18&hd=20260618: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-06-18 14:09:28,321 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=18&hd=20260618: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-06-18 14:09:41,418 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=18&hd=20260618: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-06-18 14:09:41,418 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=18&hd=20260618
2026-06-18 14:09:41,418 [ERROR] scraper: racelist fetch failed: jcd=18 rno=12
2026-06-18 14:09:41,418 [WARNING] run_cycle: fetch None: 18/12
2026-06-18 14:09:41,600 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 57
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 57
  }
]
```

## Phase別通知記録 (24h)
{'final': 20, 'result': 11, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 124
  FINAL_MISSING: 54
  PSI_DRIFT_DETECTED: 42
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 10
  CIRCUIT_BREAKER_NO_ACTION: 9
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 30 | 12 | 9,000 | 11,130 | +2,130 | 1.237 |
| S01_NAKAANA1 | 26 | 8 | 5,200 | 6,160 | +960 | 1.185 |
| S02_TETSUBAN | 14 | 7 | 2,800 | 2,140 | -660 | 0.764 |

## 直近アラート (24h・新しい順)
```
[14:04:22] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:53:39] FINAL_MISSING: {"deadline": "2026-06-18T13:23:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061817061323", "sid": "S00"}
[13:45:22] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 285, "n_recent": 70, "psi": 0.608}
[13:43:29] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.211, "baseline_mean": 0.795, "baseline_stdev": 0.071, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.583, "today_scan_count": 12, "z_score": -2.98}
[13:42:28] FINAL_MISSING: {"deadline": "2026-06-18T12:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061817041212", "sid": "S00"}
[13:41:05] FINAL_MISSING: {"deadline": "2026-06-18T13:11:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061809061311", "sid": "S00"}
[13:30:34] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.158, "baseline_mean": 0.795, "baseline_stdev": 0.071, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.636, "today_scan_count": 11, "z_score": -2.23}
[13:27:21] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 287, "n_recent": 69, "psi": 0.603}
[13:26:21] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.249, "baseline_mean": 0.795, "baseline_stdev": 0.071, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.545, "today_scan_count": 11, "z_score": -3.51}
[13:21:40] FINAL_MISSING: {"deadline": "2026-06-18T11:51:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061821081151", "sid": "S00"}
```

## 本日残レース: 85件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 71件 締切済
- 通知発射: scan=12 nid / final=8 nid / result=4 nid
- predictions: 4 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 055R | win | 1 | 0.5123 | 2.8 | 1.43 | 200 | scan=2.7 drift=+3.7% | 13:30:24 |
| S00 | 053R | win | 1 | 0.4111 | 5.0 | 2.06 | 300 | scan=4.1 drift=+22.0% | 12:32:21 |
| S01_NAKAANA1 | 172R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=- drift=- | 11:11:21 |
| S00 | 021R | win | 1 | 0.4111 | 4.4 | 1.81 | 300 | scan=4.3 drift=+2.3% | 10:44:20 |
| S01_NAKAANA1 | 014R | win | 1 | 0.5174 | 4.3 | 2.22 | 200 | scan=4.5 drift=-4.4% | 17:06:22 |
| S00 | 073R | win | 1 | 0.5123 | 7.5 | 3.84 | 300 | scan=10.5 drift=-28.6% | 16:24:21 |
| S00 | 122R | win | 1 | 0.2173 | 9.3 | 2.02 | 300 | scan=7.5 drift=+24.0% | 15:41:21 |
| S00 | 071R | win | 1 | 0.5735 | 5.5 | 3.15 | 300 | scan=4.5 drift=+22.2% | 15:22:33 |
| S01_NAKAANA1 | 0910R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=3.2 drift=-6.2% | 15:15:22 |
| S01_NAKAANA1 | 178R | win | 1 | 0.5891 | 4.0 | 2.36 | 200 | scan=- drift=- | 14:21:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 40 | -3.3% | -82.9% | +87.5% | 12 | 7 | 23 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 476.3s |
| **Latency** (scan→final max) | 609.5s |
| **Traffic** (notifications 24h) | 57 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 355 | 0.4722 | 0.3014 | +0.1708 | 🟡+36% | 0.2393 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 145 | 0.4265 | 0.2828 | 0.2197 | 🔴-0.08 | 0.804 |
| S01_NAKAANA1 | win | 132 | 0.4854 | 0.2879 | 0.2457 | 🔴-0.20 | 0.763 |
| S02_TETSUBAN | win | 78 | 0.5350 | 0.3590 | 0.2650 | 🔴-0.15 | 0.585 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 5 | 0.1835 | 0.2000 | ✅-0.0165 |
| 0.20-0.30 | 9 | 0.2241 | 0.1111 | 🔴+0.1130 |
| 0.30-0.50 | 124 | 0.4178 | 0.2581 | 🔴+0.1597 |
| 0.50+ | 207 | 0.5415 | 0.3478 | 🔴+0.1937 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 43 | 0.717 |
| win | <5.0 | ✅learned | 79 | 0.757 |
| win | <10.0 | ✅learned | 53 | 0.493 |
| win | <20.0 | ✅learned | 14 | 0.21 |
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
_auto-generated by claude_snapshot.py at 2026-06-18T14:10:02.402884+09:00_