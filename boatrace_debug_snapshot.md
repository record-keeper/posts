# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-08T11:50:01.417328+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×24 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×83 (24h)
- 🔴 PSI_DRIFT_DETECTED×24 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-05-08T11:40:26]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×5  [2026-05-08T11:27:56]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×47  [2026-05-08T11:02:20]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 ANOMALY_BET_VOLUME_DROP  ×49  [2026-05-08T10:00:09]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-08T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=12 pred=0.3328 actual=0.0833 gap=+0.2495`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-08T06:00:08]
- key: `ROI_STAT|S00: n=132 hit%=24.2% hit_CI[Bonf]=[15.2,36.3]% ROI=0.86 ROI_boot95=[0.56,1.18]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-08T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S00: n=132<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-08T06:00:08]
- key: `ORPHAN_SCAN|115 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-08T06:00:08]
- key: `DRIFT_BUCKET|drift ≤-30%: n=24 hit%=16.7% ROI=0.40 (コスト 7,200/回収 2,850)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-08T06:00:08]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=20 hit%=35.0% ROI=1.45 (コスト 6,000/回収 8,670)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-08T06:00:08]
- key: `CALIBRATION_LIVE|bt=win: n=132 pred=0.4321 actual=0.2424 error=+0.1897 (+44%) brier=0.2304 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-08T06:00:08]
- key: `CALIBRATION_LIVE|S00(win): n=132 pred=0.4321 hit=0.2424 cal_err=+0.1897 brier=0.2304 BSS=-0.25 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-08T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1887 actual=0.2000 gap=-0.0113`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-08T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2241 actual=0.3333 gap=-0.1093`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-08T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=53 pred=0.4466 actual=0.2453 gap=+0.2013`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-08T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.50+: n=49 pred=0.5325 actual=0.2653 gap=+0.2672`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-08T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-08T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=881 bet=300 odds=12.7 payout=900 ratio=0.24`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-08T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=906 bet=300 odds=14.2 payout=360 ratio=0.08`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-08T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=913 bet=300 odds=4.6 payout=2550 ratio=1.85`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.98MB / last modified 2026-05-08T11:49:28.535614+09:00

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
sed
2026-05-08 11:48:31,323 [INFO] scraper: fetch_race 18/8: boats=6 odds=189/191
2026-05-08 11:48:31,335 [INFO] predictor: CALIBRATION_MODE=on
2026-05-08 11:48:31,335 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-05-08 11:48:31,342 [INFO] run_cycle: fetched 18/8 [final]: 155 combos
2026-05-08 11:48:31,750 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-08 11:49:05,899 [INFO] run_cycle: === run_cycle 11:49:05 ===
2026-05-08 11:49:05,899 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-08 11:49:05,899 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-08 11:49:05,965 [INFO] predictor: Models loaded OK
2026-05-08 11:49:18,294 [INFO] scraper: odds3t: 120/120 parsed
2026-05-08 11:49:19,373 [INFO] scraper: odds3f: 20/20 parsed
2026-05-08 11:49:20,446 [INFO] scraper: odds2t: 30/30 parsed
2026-05-08 11:49:20,447 [INFO] scraper: odds2f: 14/15 parsed
2026-05-08 11:49:21,509 [INFO] scraper: odds_win: 5/6 parsed
2026-05-08 11:49:21,509 [INFO] scraper: fetch_race 18/8: boats=6 odds=189/191
2026-05-08 11:49:21,520 [INFO] predictor: CALIBRATION_MODE=on
2026-05-08 11:49:21,521 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-05-08 11:49:21,528 [INFO] run_cycle: fetched 18/8 [final]: 155 combos
2026-05-08 11:49:24,912 [INFO] scraper: odds3t: 120/120 parsed
2026-05-08 11:49:25,986 [INFO] scraper: odds3f: 20/20 parsed
2026-05-08 11:49:27,084 [INFO] scraper: odds2t: 30/30 parsed
2026-05-08 11:49:27,085 [INFO] scraper: odds2f: 15/15 parsed
2026-05-08 11:49:28,174 [INFO] scraper: odds_win: 5/6 parsed
2026-05-08 11:49:28,174 [INFO] scraper: fetch_race 04/1: boats=6 odds=190/191
2026-05-08 11:49:28,185 [INFO] predictor: CALIBRATION_MODE=on
2026-05-08 11:49:28,185 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-05-08 11:49:28,193 [INFO] run_cycle: fetched 04/1 [scan]: 155 combos
2026-05-08 11:49:28,469 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 26
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 26
  }
]
```

## Phase別通知記録 (24h)
{'final': 8, 'result': 6, 'scan': 12}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 83
  ANOMALY_SCRAPER_FAILURE_BURST: 39
  PSI_DRIFT_DETECTED: 24
  ANOMALY_SCAN_FINAL_RATIO: 12
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 54 | 15 | 16,200 | 15,420 | -780 | 0.952 |

## 直近アラート (24h・新しい順)
```
[11:40:26] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.555, "baseline_mean": 0.555, "baseline_stdev": 0.095, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.0, "today_scan_count": 3, "z_score": -5.85}
[11:31:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 818}
[11:29:45] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 801}
[11:28:28] FINAL_MISSING: {"deadline": "2026-05-08T10:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050813021058", "sid": "S00"}
[11:27:56] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 790}
[11:04:05] FINAL_MISSING: {"deadline": "2026-05-08T10:34:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050813011034", "sid": "S00"}
[10:49:28] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 79, "n_recent": 54, "psi": 0.452}
[10:45:42] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 79, "n_recent": 53, "psi": 0.455}
[10:38:05] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 78, "n_recent": 54, "psi": 0.512}
[10:01:05] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 77, "n_recent": 55, "psi": 0.511}
```

## 本日残レース: 114件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 30件 締切済
- 通知発射: scan=3 nid / final=1 nid / result=1 nid
- predictions: 1 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 146R | win | 1 | 0.5123 | 12.7 | 6.51 | 300 | scan=- drift=- | 10:49:20 |
| S00 | 245R | win | 1 | 0.1957 | 8.2 | 1.60 | 300 | scan=19.5 drift=-57.9% | 16:54:46 |
| S00 | 088R | win | 1 | 0.2290 | 12.0 | 2.75 | 300 | scan=6.0 drift=+100.0% | 13:53:38 |
| S00 | 1811R | win | 1 | 0.5103 | 5.0 | 2.55 | 300 | scan=5.2 drift=-3.8% | 13:32:23 |
| S00 | 053R | win | 1 | 0.4989 | 8.0 | 3.99 | 300 | scan=8.2 drift=-2.4% | 12:36:21 |
| S00 | 041R | win | 1 | 0.5334 | 9.1 | 4.85 | 300 | scan=25.6 drift=-64.5% | 11:53:20 |
| S00 | 0510R | win | 1 | 0.5123 | 6.1 | 3.13 | 300 | scan=16.5 drift=-63.0% | 16:14:22 |
| S00 | 047R | win | 1 | 0.3177 | 4.4 | 1.40 | 300 | scan=4.9 drift=-10.2% | 14:55:31 |
| S00 | 062R | win | 1 | 0.5123 | 5.5 | 2.82 | 300 | scan=4.5 drift=+22.2% | 11:57:32 |
| S00 | 072R | win | 1 | 0.4989 | 5.6 | 2.79 | 300 | scan=4.5 drift=+24.4% | 15:45:33 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 41 | -7.3% | -81.4% | +117.3% | 19 | 13 | 29 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 544.6s |
| **Latency** (scan→final max) | 626.1s |
| **Traffic** (notifications 24h) | 26 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 133 | 0.4327 | 0.2481 | +0.1846 | 🟡+43% | 0.2305 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 133 | 0.4327 | 0.2481 | 0.2305 | 🔴-0.24 | 0.867 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 5 | 0.1887 | 0.2000 | ✅-0.0113 |
| 0.20-0.30 | 9 | 0.2241 | 0.3333 | 🔴-0.1093 |
| 0.30-0.50 | 65 | 0.4256 | 0.2154 | 🔴+0.2102 |
| 0.50+ | 50 | 0.5321 | 0.2800 | 🔴+0.2521 |

## Settlement Ratio データ品質

- 学習済み: 1バンド / fallback: 15バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 6 | 0.35 |
| win | <10.0 | ✅learned | 22 | 0.564 |
| win | <20.0 | ⚠️fallback | 5 | 0.22 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-05-08T11:50:01.417328+09:00_