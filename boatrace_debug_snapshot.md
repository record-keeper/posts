# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-22T18:50:01.802453+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 FINAL_MISSING×8 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×26  [2026-05-22T18:24:06]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🔴 STRATEGY_CI_FAIL  ×45  [2026-05-22T18:05:40]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×45  [2026-05-22T18:05:40]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×36  [2026-05-22T15:30:45]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×12  [2026-05-22T11:25:31]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×35  [2026-05-22T10:00:26]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-22T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=14 pred=0.0049 actual=0.0714 gap=-0.0665`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-22T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2239 actual=0.3636 gap=-0.1397`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-22T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=5 pred=0.1288 actual=0.2000 gap=-0.0712`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-22T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S00: n=199<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-22T06:00:15]
- key: `ORPHAN_SCAN|249 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-22T06:00:15]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=38 hit%=31.6% ROI=1.31 (コスト 9,100/回収 11,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-22T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1957 actual=0.1667 gap=+0.0291`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-22T06:00:15]
- key: `ROI_STAT|S00: n=199 hit%=28.1% hit_CI[Bonf]=[20.0,38.1]% ROI=0.92 ROI_boot95=[0.70,1.19]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-22T06:00:15]
- key: `ROI_STAT|S01_NAKAANA1: n=58 hit%=32.8% hit_CI[Bonf]=[18.1,51.7]% ROI=0.87 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-22T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=58<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-22T06:00:15]
- key: `ROI_STAT|S02_TETSUBAN: n=37 hit%=43.2% hit_CI[Bonf]=[23.2,65.8]% ROI=0.81 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-22T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=37<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-22T06:00:15]
- key: `DRIFT_BUCKET|drift ≤-30%: n=48 hit%=29.2% ROI=0.80 (コスト 14,200/回収 11,400)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-22T06:00:15]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=57 hit%=28.1% ROI=0.94 (コスト 14,000/回収 13,200)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.16MB / last modified 2026-05-22T18:49:06.299954+09:00

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
ault=5000
2026-05-22 18:46:05,652 [INFO] predictor: Models loaded OK
2026-05-22 18:46:05,742 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-22 18:47:06,238 [INFO] run_cycle: === run_cycle 18:47:06 ===
2026-05-22 18:47:06,238 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-22 18:47:06,238 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-22 18:47:06,292 [INFO] predictor: Models loaded OK
2026-05-22 18:47:18,742 [INFO] scraper: odds3t: 120/120 parsed
2026-05-22 18:47:19,877 [INFO] scraper: odds3f: 20/20 parsed
2026-05-22 18:47:21,119 [INFO] scraper: odds2t: 30/30 parsed
2026-05-22 18:47:21,121 [INFO] scraper: odds2f: 15/15 parsed
2026-05-22 18:47:22,207 [INFO] scraper: odds_win: 5/6 parsed
2026-05-22 18:47:22,207 [INFO] scraper: fetch_race 15/8: boats=6 odds=190/191
2026-05-22 18:47:22,219 [INFO] predictor: CALIBRATION_MODE=on
2026-05-22 18:47:22,219 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-05-22 18:47:22,226 [INFO] run_cycle: fetched 15/8 [scan]: 155 combos
2026-05-22 18:47:22,324 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-22 18:48:06,115 [INFO] run_cycle: === run_cycle 18:48:06 ===
2026-05-22 18:48:06,116 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-22 18:48:06,116 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-22 18:48:06,206 [INFO] predictor: Models loaded OK
2026-05-22 18:48:06,310 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-22 18:49:06,068 [INFO] run_cycle: === run_cycle 18:49:06 ===
2026-05-22 18:49:06,069 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-22 18:49:06,069 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-22 18:49:06,128 [INFO] predictor: Models loaded OK
2026-05-22 18:49:06,216 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 53
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 53
  }
]
```

## Phase別通知記録 (24h)
{'final': 21, 'result': 15, 'scan': 17}

## アラート件数 (24h・種類別)
```
  KS_ODDS_DRIFT: 40
  ANOMALY_SCRAPER_FAILURE_BURST: 29
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 8
  FINAL_MISSING: 8
  ANOMALY_BET_VOLUME_SPIKE: 3
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 30 | 12 | 9,000 | 13,980 | +4,980 | 1.553 |
| S01_NAKAANA1 | 27 | 7 | 5,400 | 5,420 | +20 | 1.004 |
| S02_TETSUBAN | 13 | 5 | 2,600 | 1,640 | -960 | 0.631 |

## 直近アラート (24h・新しい順)
```
[18:24:06] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.001815, "ks_stat": 0.251}
[18:05:40] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[18:00:44] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 8.7, "baseline_n_days": 7, "baseline_stdev": 2.9, "hour": 18, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 15, "z_score": 2.15}
[17:58:29] FINAL_MISSING: {"deadline": "2026-05-22T11:25:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052209031125", "sid": "S00"}
[17:56:06] FINAL_MISSING: {"deadline": "2026-05-22T17:26:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052201051726", "sid": "S00"}
[17:23:47] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.001815, "ks_stat": 0.251}
[17:23:47] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 8.6, "baseline_n_days": 7, "baseline_stdev": 3.1, "hour": 17, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 15, "z_score": 2.07}
[17:05:22] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[16:59:34] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.002565, "ks_stat": 0.246}
[16:57:06] FINAL_MISSING: {"deadline": "2026-05-22T11:25:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052209031125", "sid": "S00"}
```

## 本日残レース: 18件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 114件 締切済
- 通知発射: scan=16 nid / final=20 nid / result=15 nid
- predictions: 15 / うち結果DB記録済: 15
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 015R | win | 1 | 0.4111 | 4.2 | 1.73 | 200 | scan=3.2 drift=+31.2% | 17:23:45 |
| S01_NAKAANA1 | 014R | win | 1 | 0.5123 | 3.4 | 1.74 | 200 | scan=- drift=- | 16:59:33 |
| S01_NAKAANA1 | 013R | win | 1 | 0.3177 | 3.1 | 0.98 | 200 | scan=- drift=- | 16:25:21 |
| S01_NAKAANA1 | 152R | win | 1 | 0.5123 | 4.5 | 2.31 | 200 | scan=3.7 drift=+21.6% | 16:04:21 |
| S00 | 011R | win | 1 | 0.3177 | 4.6 | 1.46 | 300 | scan=18.3 drift=-74.9% | 15:22:45 |
| S01_NAKAANA1 | 055R | win | 1 | 0.4111 | 4.2 | 1.73 | 200 | scan=- drift=- | 13:42:21 |
| S00 | 097R | win | 1 | 0.4111 | 6.7 | 2.75 | 300 | scan=5.6 drift=+19.6% | 13:21:32 |
| S00 | 087R | win | 1 | 0.4111 | 5.0 | 2.06 | 300 | scan=- drift=- | 13:10:24 |
| S01_NAKAANA1 | 096R | win | 1 | 0.5174 | 3.7 | 1.91 | 200 | scan=3.7 drift=+0.0% | 12:49:20 |
| S02_TETSUBAN | 114R | win | 1 | 0.5334 | 2.8 | 1.49 | 200 | scan=- drift=- | 11:59:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 39 | +4.1% | -74.9% | +148.9% | 14 | 7 | 30 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 470.1s |
| **Latency** (scan→final max) | 617.8s |
| **Traffic** (notifications 24h) | 53 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |
| **Saturation** (S01_NAKAANA1) | 1,200円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 299 | 0.4566 | 0.3144 | +0.1423 | 🟡+31% | 0.2324 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 195 | 0.4370 | 0.2821 | 0.2261 | 🔴-0.12 | 0.948 |
| S01_NAKAANA1 | win | 64 | 0.4814 | 0.3281 | 0.2386 | 🔴-0.08 | 0.863 |
| S02_TETSUBAN | win | 40 | 0.5126 | 0.4500 | 0.2529 | 🔴-0.02 | 0.83 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 13 | 0.0041 | 0.0769 | 🔴-0.0729 |
| 0.10-0.15 | 5 | 0.1288 | 0.2000 | 🔴-0.0712 |
| 0.15-0.20 | 6 | 0.1957 | 0.1667 | ✅+0.0291 |
| 0.20-0.30 | 12 | 0.2243 | 0.3333 | 🔴-0.1090 |
| 0.30-0.50 | 133 | 0.4199 | 0.2406 | 🔴+0.1793 |
| 0.50+ | 141 | 0.5394 | 0.3972 | 🔴+0.1423 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 18 | 0.755 |
| win | <5.0 | ✅learned | 37 | 0.806 |
| win | <10.0 | ✅learned | 32 | 0.544 |
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
_auto-generated by claude_snapshot.py at 2026-05-22T18:50:01.802453+09:00_