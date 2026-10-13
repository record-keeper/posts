# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-13T10:50:02.024063+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×23 (24h)
- 🔴 PSI_DRIFT_DETECTED×17 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×1  [2026-10-13T10:47:58]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×9  [2026-10-13T10:39:21]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 STRATEGY_CI_FAIL  ×47  [2026-10-13T10:01:10]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×18  [2026-10-13T10:00:39]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-13T06:00:25]
- key: `INSUFFICIENT_SAMPLE|S00: n=177<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-13T06:00:25]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=83<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-13T06:00:25]
- key: `ORPHAN_SCAN|164 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-13T06:00:25]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=168<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-10-13T06:00:25]
- key: `ROI_STAT|S00: n=177 hit%=24.3% hit_CI[Bonf]=[16.3,34.6]% ROI=0.67 ROI_boot95=[0.47,0.89]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-13T06:00:25]
- key: `ROI_STAT|S01_NAKAANA1: n=168 hit%=35.1% hit_CI[Bonf]=[25.4,46.2]% ROI=1.06 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-13T06:00:25]
- key: `ROI_STAT|S02_TETSUBAN: n=83 hit%=50.6% hit_CI[Bonf]=[35.4,65.7]% ROI=0.90 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-13T06:00:25]
- key: `DRIFT_BUCKET|drift ≤-30%: n=31 hit%=38.7% ROI=1.09 (コスト 9,000/回収 9,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-13T06:00:25]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=51 hit%=31.4% ROI=0.75 (コスト 12,100/回収 9,020)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-13T06:00:25]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=89 hit%=34.8% ROI=0.91 (コスト 20,400/回収 18,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-13T06:00:25]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=57 hit%=36.8% ROI=0.90 (コスト 13,400/回収 12,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-13T06:00:25]
- key: `DRIFT_BUCKET|drift ≥+30%: n=42 hit%=23.8% ROI=0.74 (コスト 10,900/回収 8,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-13T06:00:25]
- key: `CALIBRATION_LIVE|bt=win: n=428 pred=0.4819 actual=0.3364 error=+0.1454 (+30%) brier=0.2507 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-13T06:00:25]
- key: `CALIBRATION_LIVE|S00(win): n=177 pred=0.4515 hit=0.2429 cal_err=+0.2086 brier=0.2510 BSS=-0.36 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-13T06:00:25]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=168 pred=0.4917 hit=0.3512 cal_err=+0.1405 brier=0.2474 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-13T06:00:25]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=83 pred=0.5265 hit=0.5060 cal_err=+0.0205 brier=0.2569 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 15.68MB / last modified 2026-10-13T10:48:01.128008+09:00

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
bos: {'win': 6, '2t': 30, '3t': 120}
2026-10-13 10:47:55,219 [INFO] run_cycle: fetched 04/2 [scan]: 156 combos
2026-10-13 10:47:55,443 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-13 10:49:04,586 [INFO] run_cycle: === run_cycle 10:49:04 ===
2026-10-13 10:49:04,586 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-13 10:49:04,586 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-13 10:49:04,617 [INFO] predictor: Models loaded OK
2026-10-13 10:49:15,649 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=14&hd=20261013: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-13 10:49:26,738 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=14&hd=20261013: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-10-13 10:49:39,800 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=14&hd=20261013: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-10-13 10:49:39,800 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=14&hd=20261013
2026-10-13 10:49:39,800 [ERROR] scraper: racelist fetch failed: jcd=14 rno=6
2026-10-13 10:49:39,800 [WARNING] run_cycle: fetch None: 14/6
2026-10-13 10:49:50,984 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=1&jcd=06&hd=20261013: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-13 10:50:02,685 [INFO] scraper: odds3t: 120/120 parsed
2026-10-13 10:50:03,913 [INFO] scraper: odds3f: 20/20 parsed
2026-10-13 10:50:05,056 [INFO] scraper: odds2t: 30/30 parsed
2026-10-13 10:50:05,059 [INFO] scraper: odds2f: 15/15 parsed

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
    "c": 89
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 89
  }
]
```

## Phase別通知記録 (24h)
{'final': 37, 'result': 20, 'scan': 32}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 280
  FINAL_MISSING: 23
  ANOMALY_BET_VOLUME_SPIKE: 18
  PSI_DRIFT_DETECTED: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 2
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 37 | 10 | 11,100 | 8,850 | -2,250 | 0.797 |
| S01_NAKAANA1 | 39 | 15 | 7,800 | 6,720 | -1,080 | 0.862 |
| S02_TETSUBAN | 21 | 10 | 4,200 | 3,700 | -500 | 0.881 |

## 直近アラート (24h・新しい順)
```
[10:47:55] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 724}
[10:39:21] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.506, "baseline_mean": 0.84, "baseline_stdev": 0.097, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.333, "today_scan_count": 3, "z_score": -5.25}
[10:18:46] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": 33.3, "final": 4.0, "kind": "LARGE_ODDS_DRIFT", "race": "145R", "scan": 3.0, "sid": "S01_NAKAANA1"}
[10:01:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:00:31] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 1.8, "baseline_n_days": 4, "baseline_stdev": 0.5, "hour": 10, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 0, "z_score": -3.5}
[09:01:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:00:43] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:16:03] FINAL_MISSING: {"deadline": "2026-10-12T11:39:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101218071139", "sid": "S00"}
[23:09:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 118件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 14件 締切済
- 通知発射: scan=3 nid / final=2 nid / result=0 nid
- predictions: 2 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 131R | win | 1 | 0.5891 | 3.0 | 1.77 | 200 | scan=- drift=- | 10:43:20 |
| S01_NAKAANA1 | 145R | win | 1 | 0.4111 | 4.0 | 1.64 | 200 | scan=3.0 drift=+33.3% | 10:18:44 |
| S00 | 196R | win | 1 | 0.5174 | 4.0 | 2.07 | 300 | scan=- drift=- | 19:53:31 |
| S01_NAKAANA1 | 194R | win | 1 | 0.4111 | 4.3 | 1.77 | 200 | scan=3.6 drift=+19.4% | 19:01:19 |
| S00 | 194R | win | 1 | 0.4111 | 4.3 | 1.77 | 300 | scan=9.0 drift=-52.2% | 19:01:17 |
| S00 | 193R | win | 1 | 0.2290 | 7.2 | 1.65 | 300 | scan=7.4 drift=-2.7% | 18:31:20 |
| S02_TETSUBAN | 166R | win | 1 | 0.5998 | 2.7 | 1.62 | 200 | scan=- drift=- | 13:37:30 |
| S00 | 066R | win | 1 | 0.3177 | 6.0 | 1.91 | 300 | scan=5.2 drift=+15.4% | 13:17:31 |
| S01_NAKAANA1 | 2310R | win | 1 | 0.4111 | 3.3 | 1.36 | 200 | scan=- drift=- | 13:04:19 |
| S00 | 225R | win | 1 | 0.1034 | 6.9 | 0.71 | 300 | scan=- drift=- | 12:57:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 58 | +12.0% | -60.0% | +326.7% | 15 | 6 | 39 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 491.4s |
| **Latency** (scan→final max) | 658.3s |
| **Traffic** (notifications 24h) | 89 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 427 | 0.4818 | 0.3372 | +0.1445 | 🟡+30% | 0.2507 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 177 | 0.4515 | 0.2429 | 0.2510 | 🔴-0.36 | 0.671 |
| S01_NAKAANA1 | win | 167 | 0.4915 | 0.3533 | 0.2472 | 🔴-0.08 | 1.065 |
| S02_TETSUBAN | win | 83 | 0.5265 | 0.5060 | 0.2569 | 🔴-0.03 | 0.901 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.20-0.30 | 5 | 0.2245 | 0.2000 | ✅+0.0245 |
| 0.30-0.50 | 156 | 0.4177 | 0.3013 | 🔴+0.1164 |
| 0.50+ | 254 | 0.5436 | 0.3622 | 🔴+0.1814 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 178 | 0.771 |
| win | <5.0 | ✅learned | 318 | 0.757 |
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
_auto-generated by claude_snapshot.py at 2026-10-13T10:50:02.024063+09:00_